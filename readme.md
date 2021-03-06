# Pyventure is a simple library for creating a text adventure with Python
I created this library with and for my son for him to practice coding,
using pip, and importing libraries.


## Installation
`python -m pip install pyventure`

## Tutorial
Pyventure handles the game logic; all the user needs to do is
create `Place` objects. Each `Place` object represents a location
on the game map. It is the game space which includes things with 
which the player can interact.

A `Place` object is created by providing four parameters:
1. a string `name` _required_
2. a string `description` _required_
3. a list of `Feature`s
4. a list of `Node`s

### Example of a playable game with two places to move between
```python
from pyventure.place import Place, Feature, Node
from pyventure.items import Clue, Consumable, Tool
from pyventure.game_loops import start
from pyventure.message import msg

LIVING_ROOM = 'Living Room'
KITCHEN = 'Kitchen'

living_room = Place(
    name=LIVING_ROOM,
    description="There is a door on your [u]left[/u] and a pencil on the carpet.",
    features=[
        Feature(
            name='pencil',
            interact_msg='It is a no. 2 Pencil',
            takeable=Tool(
                name='pencil',
                risk=0,
                uses=10,
                description='it could stand to be sharpened',
                total=1
            )
        )
    ],
    nodes = [
        Node(
            name='left',
            place_name=KITCHEN,
            travel_msg='You open the door and stop into the kitchen.',
            accessible=True
        )
    ]
)


kitchen = Place(
    name=KITCHEN,
    description="The floor is dirty. You're afraid of what is in the refridgerator.",
    features=[],
    nodes = [
        Node(
            name='living room',
            place_name=LIVING_ROOM,
            travel_msg='You are back in the living room.',
            accessible=True
        )
    ]
)

all_places = {
    LIVING_ROOM: living_room,
    KITCHEN: kitchen
}


if __name__ == '__main__':
    msg.narrate('Welcome to a Simple Game')
    start(new_game_msg='Name your character: ', all_places=all_places)

```
