This RFC exmplains the basic system on how communication between client and server will work. The main premise is that should use a **event driven** architecture. This architecture must be powered by both requests and responses been tracked through a messaging queue system.

Here is an example of a communication:

 * The player requests an action using the UI interface (like draw a card from the desk).
 * An HTTP Request will be sent to the server API.
 * The server will acknowledge the parameters and saves the request in a messaging queue (like RabbitMQ).
 * The server acknowledge the request and sends a 200 OK response.
 * Once a server is free will fetch the request from the messaging queue and start processing.
 * It will change the state of the game, always keeping track of the new changes in the DB layer
 * Once finished processing will send the update to a messaging queue.
 * This messaging queue will send the update state to the player/s through websockets.
 * Also other microservices (like the AI bot one) might also fetch the new state.

It is imperative to understand that some of the events in the messaging queue might block processing further requests, for example a player might not start another action until we ensure that the opponent have finished processing the animations for the previous ones.

Which is why some requests might hold the 200 response for a few seconds, but then, we might invalidate the waiting and flag as one of the players as unavailable.

Also, events can be discarded, the player will always be able to refresh the page and re-request the full state from the DB.
