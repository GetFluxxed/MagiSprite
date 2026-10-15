# Original user brief

Source: the owner’s “Design Sprite Roguelite” discussion, retrieved in full for preproduction. The returned brief text below is preserved, including HTML space entities. Private conversation identifiers are omitted from this repository header. This is source reference material.

I have another ambition to start a mobile game. I want to make something with an addictive game loop. I want it to be a creature collecting roguelite. Kind of like if Pokemon was Final Fantasy. It needs to be rather fast paced, with streamlined gameplay, smooth frames, interesting combat, and needs narrative direction and art.&#x20;
The roguelite aspect or carry over from run to run should be Mage Power as well as a Sprite Book.

I want the sprite book to look almost like a dossier entry book in concept, and it will fill out each of the sprites you find as you journey, with undiscovered Sprite Pages not in the book until that sprite is discovered and you get to make an entry on it by capturing or defeating it. If you collect a sprite 'x' amount of times, perhaps another roguelite mechanic is you start to find stronger/elite variants of previous sprites. This could keep players engaged in finding stronger and stronger things to further there highscores/progress and give builds a good sense of continued diversity.

As you play with a specific mage more and more, they gain exp and earn mage specific levels. These levels will unlock points in a greater skill tree. To test we will make the tree's very small and manageable and expand as we test.&#x20;

Before we create or develop anything, I want to flush out mechanics that I want to include, as well as design the items, creatures, characters, game loop, etc before any code is truly done.&#x20;

The creatures are going to need a name, like how Pokemon is pokemon, in Palmon they are Pals. I want to name them that ties into their lore correctly somehow, as in maybe the world is named after the creatures. Actually, I just want them to be Sprites. I want that to be their names, Sprites. Maybe this can change as we go, and the character you play as is a Sprite Mage.&#x20;

Sprite Mages are able to develop bonds with various sprites, this is the collection aspect that I want, though whether or not they can bond is determined by what stats the player currently has. I want different types of base Mages that players can unlock, kind of similar to how Risk of Rain 2 has unlockable character archetypes. Each Sprite Mage has different affinities, boosts, or builds that synergize with them best. The basic Sprite Mage should be able to do everything, the unlockable or alternative mages will have specific drawbacks and downsides, but the baseline should be fun for anyone.&#x20;

I want an element system within the game to determine strengths and weaknesses of specific sprites against others. Perhaps 6 colors, Fire > Grass > Water as the main three and most abundant elements, 2 rarer types which are effective against each other perhaps Void and Space Sprites, these should be rarely obtainable, and then a 6th standalone that has no default weakness or strength, but can maybe learn moves from all 6 types, called Prismatic Sprites.&#x20;

We can pull some slight inspiration from games like Summoners War in how they upgrade their summons, players may find "Sprite Food" to upgrade their sprites during their runs. Different sprite foods drop at different rates, and gives their sprite a corresponding amount of exp and different rarities or types of foods might be better if given to specific elemental sprites.&#x20;

We will attach drops to a robust drop table, sorted by rarity.&#x20;
To start, we will have 4 different rarity types:
Common - Grey
Uncommon - Green
Rare - Blue
Legendary - Gold&#x20;

We will develop this in the future of course, but for the drop tables, each rarity has its own table that gets rolled first. For example, we might have 40% chance for normal, 30% chance for uncommon, 20% chance for rare, 10% chance for legendary to start out. Starting with rolling for selection on legendary, if the drop should not be legendary, it will cascade to the rare table. If it succeeds on rare drop, we then roll through all of the possible rare items within the pool. This allows us to edit drops within each pool without throwing off the odds for anything outside each pool. &#x20;

I'm not sure the game art direction or design necessarily, I do for sure want a form of pixel art, and while I do like the different pixel art styles, I want to kind of take inspiration from Octopath Traveler 1 and 2, older Final Fantasy titles like from Final Fantasy 1 and 2, and for combat I like the Final Fantasy style layout, turn based, team focused, targeting and selecting, different actions per sprite per individual turn, individual skillsets, consumables, etc.

With all of this create for me 3 documents. Create a "ARCHITECTURE.md" file, that will include the current information I have provided, a DESIGN.md file that is a version of architecture.md that you have interpreted and expanded on, and a folder that contains wireframes/visuals of what different parts of the game could look like, such as a sketched version of a sprite, a sprite mage, a combat sequence, idle in the game world, etc. There is a file called ENGINEERING.md found in the Portfolio Website Planning project that I would like you to also have within the code base for this project.&#x20;
