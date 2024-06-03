## Dragon Booster Game

Dragon Booster Game is a simple, interactive text-based adventure game where players can explore different locations, buy items, fight monsters, and gain experience. The game uses HTML, CSS, JavaScript, and Shepherd.js for a guided tour of the game's features.

### Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Code Overview](#code-overview)
- [Shepherd.js Tour](#shepherdjs-tour)
- [Contributing](#contributing)
- [License](#license)

### Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/dragon-booster-game.git
   cd dragon-booster-game
   ```

2. **Open the project in your preferred code editor**.

3. **Open the `index.html` file in a web browser** to start the game.

### Usage

1. **Start the game** by opening `index.html` in your browser.
2. **Explore the game**:
   - Use the buttons to navigate to different locations like the store, cave, and town square.
   - Buy health and weapons in the store using gold.
   - Fight monsters in the cave to gain experience and gold.
   - Defeat the dragon to win the game.
3. **Guided Tour**: Click the "Start Tour" button to get an interactive guide through the game's interface and features.

### Features

- **Interactive Text-Based Adventure**: Navigate through various locations, make choices, and experience different outcomes.
- **Inventory Management**: Buy and sell weapons, manage your health, and collect gold.
- **Monster Battles**: Fight against different monsters with varying difficulty levels.
- **Guided Tour**: An interactive tour using Shepherd.js to help new players understand the game mechanics.

### Code Overview

The game consists of the following main components:

1. **HTML (index.html)**:
   - Defines the structure of the game interface.
   - Includes Shepherd.js library and CSS for the guided tour.

2. **CSS (style.css)**:
   - Styles the game interface for a clean and user-friendly experience.

3. **JavaScript (script.js)**:
   - Contains the game logic including navigation, buying items, fighting monsters, and managing inventory.
   - Integrates Shepherd.js for the guided tour.

#### JavaScript Functions

- **update(location)**: Updates the game interface based on the current location.
- **goTown, goStore, goCave**: Navigation functions for different locations.
- **buyHealth, buyWeapon, sellWeapon**: Functions to manage player's health and inventory.
- **fightSlime, fightBeast, fightDragon**: Functions to initiate battles with different monsters.
- **attack, dodge**: Functions to handle combat actions.
- **defeatMonster, lose, winGame, restart**: Functions to handle game outcomes.
- **easterEgg, pickTwo, pickEight, pick**: Functions for a secret mini-game.

### Shepherd.js Tour

The Shepherd.js tour guides new players through the game's interface, explaining key features and how to start playing. It includes steps to introduce the stats, inventory, game events, action buttons, and initial actions.

### Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**.
2. **Create a new branch** for your feature or bug fix.
   ```sh
   git checkout -b feature/your-feature-name
   ```
3. **Commit your changes**.
   ```sh
   git commit -m "Add your message here"
   ```
4. **Push to the branch**.
   ```sh
   git push origin feature/your-feature-name
   ```
5. **Create a pull request** describing your changes.

### License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
![image](https://github.com/Amarnath-Rao/q12-dragon-booster/assets/96937608/9fb2827c-797a-41c4-beb7-963738de893c)


### Code:

```
let xp = 0;
let health = 100;
let gold = 50;
let currentWeapon = 0;
let fighting;
let monsterHealth;
let inventory = ["stick"];

const button1 = document.querySelector("#button1");
const button2 = document.querySelector("#button2");
const button3 = document.querySelector("#button3");
const text = document.querySelector("#text");
const xpText = document.querySelector("#xpText");
const healthText = document.querySelector("#healthText");
const goldText = document.querySelector("#goldText");
const monsterStats = document.querySelector("#monsterStats");
const monsterNameText = document.querySelector("#monsterName");
const monsterHealthText = document.querySelector("#monsterHealth");
const startTourBtn = document.querySelector("#startTourBtn");

const weapons = [
    { name: "stick", power: 5 },
    { name: "dagger", power: 30 },
    { name: "claw hammer", power: 50 },
    { name: "sword", power: 100 }
];

const monsters = [
    { name: "slime", level: 2, health: 15 },
    { name: "fanged beast", level: 8, health: 60 },
    { name: "dragon", level: 20, health: 300 }
];

const locations = [
    {
        name: "town square",
        "button text": ["Go to store", "Go to cave", "Fight dragon"],
        "button functions": [goStore, goCave, fightDragon],
        text: 'You are in the town square. You see a sign that says "Store."'
    },
    {
        name: "store",
        "button text": ["Buy 10 health (10 gold)", "Buy weapon (30 gold)", "Go to town square"],
        "button functions": [buyHealth, buyWeapon, goTown],
        text: "You enter the store."
    },
    {
        name: "cave",
        "button text": ["Fight slime", "Fight fanged beast", "Go to town square"],
        "button functions": [fightSlime, fightBeast, goTown],
        text: "You enter the cave. You see some monsters."
    },
    {
        name: "fight",
        "button text": ["Attack", "Dodge", "Run"],
        "button functions": [attack, dodge, goTown],
        text: "You are fighting a monster."
    },
    {
        name: "kill monster",
        "button text": ["Go to town square", "Go to town square", "Go to town square"],
        "button functions": [goTown, goTown, easterEgg],
        text: 'The monster screams "Arg!" as it dies. You gain experience points and find gold.'
    },
    {
        name: "lose",
        "button text": ["REPLAY?", "REPLAY?", "REPLAY?"],
        "button functions": [restart, restart, restart],
        text: "You die. ☠️"
    },
    {
        name: "win",
        "button text": ["REPLAY?", "REPLAY?", "REPLAY?"],
        "button functions": [restart, restart, restart],
        text: "You defeat the dragon! YOU WIN THE GAME! 🎉"
    },
    {
        name: "easter egg",
        "button text": ["2", "8", "Go to town square?"],
        "button functions": [pickTwo, pickEight, goTown],
        text: "You find a secret game. Pick a number above. Ten numbers will be randomly chosen between 0 and 10. If the number you choose matches one of the random numbers, you win!"
    }
];

// Initialize buttons
button1.onclick = goStore;
button2.onclick = goCave;
button3.onclick = fightDragon;

startTourBtn.onclick = startTour;

function update(location) {
    monsterStats.style.display = "none";
    button1.innerText = location["button text"][0];
    button2.innerText = location["button text"][1];
    button3.innerText = location["button text"][2];
    button1.onclick = location["button functions"][0];
    button2.onclick = location["button functions"][1];
    button3.onclick = location["button functions"][2];
    text.innerText = location.text;
}

function goTown() {
    update(locations[0]);
}

function goStore() {
    update(locations[1]);
}

function goCave() {
    update(locations[2]);
}

function buyHealth() {
    if (gold >= 10) {
        gold -= 10;
        health += 10;
        goldText.innerText = gold;
        healthText.innerText = health;
    } else {
        text.innerText = "You do not have enough gold to buy health.";
    }
}

function buyWeapon() {
    if (currentWeapon < weapons.length - 1) {
        if (gold >= 30) {
            gold -= 30;
            currentWeapon++;
            goldText.innerText = gold;
            let newWeapon = weapons[currentWeapon].name;
            text.innerText = "You now have a " + newWeapon + ".";
            inventory.push(newWeapon);
            text.innerText += " In your inventory you have: " + inventory;
        } else {
            text.innerText = "You do not have enough gold to buy a weapon.";
        }
    } else {
        text.innerText = "You already have the most powerful weapon!";
        button2.innerText = "Sell weapon for 15 gold";
        button2.onclick = sellWeapon;
    }
}

function sellWeapon() {
    if (inventory.length > 1) {
        gold += 15;
        goldText.innerText = gold;
        let currentWeapon = inventory.shift();
        text.innerText = "You sold a " + currentWeapon + ".";
        text.innerText += " In your inventory you have: " + inventory;
    } else {
        text.innerText = "Don't sell your only weapon!";
    }
}

function fightSlime() {
    fighting = 0;
    goFight();
}

function fightBeast() {
    fighting = 1;
    goFight();
}

function fightDragon() {
    fighting = 2;
    goFight();
}

function goFight() {
    update(locations[3]);
    monsterHealth = monsters[fighting].health;
    monsterStats.style.display = "block";
    monsterNameText.innerText = monsters[fighting].name;
    monsterHealthText.innerText = monsterHealth;
}

function attack() {
    text.innerText = "The " + monsters[fighting].name + " attacks.";
    text.innerText += " You attack it with your " + weapons[currentWeapon].name + ".";

    if (isMonsterHit()) {
        health -= getMonsterAttackValue(monsters[fighting].level);
    } else {
        text.innerText += " You miss.";
    }

    monsterHealth -= weapons[currentWeapon].power + Math.floor(Math.random() * xp) + 1;
    healthText.innerText = health;
    monsterHealthText.innerText = monsterHealth;
    if (health <= 0) {
        lose();
    } else if (monsterHealth <= 0) {
        fighting === 2 ? winGame() : defeatMonster();
    }

    if (Math.random() <= 0.1 && inventory.length !== 1) {
        text.innerText += " Your " + inventory.pop() + " breaks.";
        currentWeapon--;
    }
}

function getMonsterAttackValue(level) {
    let hit = level * 5 - Math.floor(Math.random() * xp);
    return hit;
}

function isMonsterHit() {
    return Math.random() > 0.2 || health < 20;
}

function dodge() {
    text.innerText = "You dodge the attack from the " + monsters[fighting].name + ".";
}

function defeatMonster() {
    gold += Math.floor(monsters[fighting].level * 6.7);
    xp += monsters[fighting].level;
    goldText.innerText = gold;
    xpText.innerText = xp;
    update(locations[4]);
}

function lose() {
    update(locations[5]);
}

function winGame() {
    update(locations[6]);
}

function restart() {
    xp = 0;
    health = 100;
    gold = 50;
    currentWeapon = 0;
    inventory = ["stick"];
    goldText.innerText = gold;
    healthText.innerText = health;
    xpText.innerText = xp;
    goTown();
}

function easterEgg() {
    update(locations[7]);
}

function pickTwo() {
    pick(2);
}

function pickEight() {
    pick(8);
}

function pick(guess) {
    let numbers = [];
    while (numbers.length < 10) {
        numbers.push(Math.floor(Math.random() * 11));
    }

    text.innerText = "You picked " + guess + ". Here are the random numbers:\n";

    for (let i = 0; i < 10; i++) {
        text.innerText += numbers[i] + "\n";
    }

    if (numbers.indexOf(guess) !== -1) {
        text.innerText += "Right! You win 20 gold!";
        gold += 20;
        goldText.innerText = gold;
    } else {
        text.innerText += "Wrong! You lose 10 health!";
        health -= 10;
        healthText.innerText = health;
        if (health <= 0) {
            lose();
        }
    }
}

// Shepherd.js Tour
function startTour() {
    const tour = new Shepherd.Tour({
        useModalOverlay: true,
        defaultStepOptions: {
            cancelIcon: {
                enabled: true
            },
            classes: 'shadow-md bg-purple-dark',
            scrollTo: true
        }
    });

    tour.addStep({
        id: 'intro',
        text: 'Welcome to the Adventure Game! Let\'s take a quick tour.',
        attachTo: {
            element: '#app',
            on: 'bottom'
        },
        buttons: [
            {
                text: 'Next',
                action: tour.next
            }
        ]
    });

    tour.addStep({
        id: 'stats',
        text: 'Here you can see your stats: XP, Health, and Gold.',
        attachTo: {
            element: '#stats',
            on: 'bottom'
        },
        buttons: [
            {
                text: 'Next',
                action: tour.next
            }
        ]
    });

    tour.addStep({
        id: 'inventory',
        text: 'This is your inventory. You start with a stick.',
        attachTo: {
            element: '#inventory',
            on: 'bottom'
        },
        buttons: [
            {
                text: 'Next',
                action: tour.next
            }
        ]
    });

    tour.addStep({
        id: 'text',
        text: 'This area displays the current game events and actions.',
        attachTo: {
            element: '#text',
            on: 'top'
        },
        buttons: [
            {
                text: 'Next',
                action: tour.next
            }
        ]
    });

    tour.addStep({
        id: 'buttons',
        text: 'Use these buttons to navigate and perform actions.',
        attachTo: {
            element: '#buttons',
            on: 'top'
        },
        buttons: [
            {
                text: 'Next',
                action: tour.next
            }
        ]
    });

    tour.addStep({
        id: 'start',
        text: 'Click "Go to store" to start your adventure!',
        attachTo: {
            element: '#button1',
            on: 'right'
        },
        buttons: [
            {
                text: 'Finish',
                action: tour.complete
            }
        ]
    });

    tour.start();
}

```
