# Rock Paper Scissors

A browser-based Rock Paper Scissors game. The backend is written in **Java** using object-oriented design and served with **Spring Boot**, and the UI is built with **Vue 3**.

Play against the computer on two difficulty levels:
- **Easy**: the computer picks a random move.
- **Hard**: the computer counts which move you play most and plays the move that beats it.

## Tech stack
| Part | Technology |
|---|---|
| Language | Java 17+ |
| Backend | Spring Boot 3 (REST API) |
| Frontend | Vue 3 (loaded from a CDN, no build step) |
| Build | Maven |
| Tests | JUnit 5 |

## Run it
Requires Java 17+ and Maven.
```bash
mvn spring-boot:run
```
Then open http://localhost:8080.

```bash
mvn test       # run the unit tests
mvn package    # build target/rock-paper-scissors-1.0.0.jar
```

## Project structure
```
src/main/java/com/example/rps/
├── model/        Move, Outcome, Round, Scoreboard, Game   (rules and state)
├── player/       Player (abstract), HumanPlayer, ComputerPlayer
├── strategy/     MoveStrategy, RandomStrategy, FrequencyStrategy, Difficulty
├── service/      GameService
├── dto/          request/response records
└── controller/   GameController (REST API)
src/main/resources/static/   index.html + style.css (Vue UI)
src/test/java/...            GameLogicTest
docs/                        explanation PDF, source-code PDF, presentation
```

## REST API
| Method & URL | Body | Description |
|---|---|---|
| `POST /api/games` | `{"playerName": "...", "difficulty": "EASY"}` | Start a new game |
| `GET /api/games/{id}` | – | Get the game state |
| `POST /api/games/{id}/play` | `{"move": "ROCK"}` | Play one round |
| `POST /api/games/{id}/reset` | – | Reset the score |

## OOP concepts used
- **Abstraction**: the abstract `Player` class and the `MoveStrategy` interface
- **Encapsulation**: `Scoreboard` and `Game` keep their state private
- **Inheritance**: `HumanPlayer` and `ComputerPlayer` extend `Player`
- **Polymorphism**: `chooseMove()` / `nextMove()` behave differently for each player and strategy
- **Composition**: a `Game` has players, a scoreboard and rounds
- **Strategy pattern**: the computer's AI is a pluggable `MoveStrategy`

## Documentation
- [`docs/1-Project-Explanation.pdf`](docs/1-Project-Explanation.pdf): module-by-module explanation
- [`docs/2-Source-Code.pdf`](docs/2-Source-Code.pdf): full source listing
- [`docs/Rock-Paper-Scissors-Presentation.pptx`](docs/Rock-Paper-Scissors-Presentation.pptx): 5-slide overview
