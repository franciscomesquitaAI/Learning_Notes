The Game of Life is a cellular automaton devised by the British mathematician John Horton Conway in 1970. It is the best-known example of a cellular automaton. The "game" is actually a zero-player game, meaning that its evolution is determined by its initial state, needing no input from human players. One interacts with the Game of Life by creating an initial configuration and observing how it evolves.


# Why is this relevant?

Conway’s Game of Life is fascinating because **it demonstrates how simple rules can lead to complex and emergent behavior**, which an essential concept in artificial life, complexity theory, and computational science. In computing, it has inspired research in algorithms, artificial intelligence, and self-replicating systems, while also serving as a classic example of how order can emerge from chaos.

Look at how fascinating these patterns can be \[1]:

![Game Of Life example image1](https://i.imgur.com/gbbmSeG.png)


---

# How it works?

The universe of the Game of Life is an infinite two-dimensional orthogonal grid of square cells, each of which is in one of two possible states, live or dead. Every cell interacts with its eight neighbours, which are the cells that are directly horizontally, vertically, or diagonally adjacent \[2]. At each step in time, the following transitions occur \[3]:

1. Any live cell with fewer than two live neighbours dies, as if by underpopulation.

2. Any live cell with two or three live neighbours lives on to the next generation.

3. Any live cell with more than three live neighbours dies, as if by overpopulation.

4. Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.


The image below ilustrates these rules:

![Game Of Life rules representation](https://i.imgur.com/x7UPYIv.png)


An amazing explanation of the concept from the creator itself (John Conway) can be seen here: [https://www.youtube.com/watch?v=R9Plq-D1gEk](https://www.youtube.com/watch?v=R9Plq-D1gEk)

---

# My own implementation

I used python with some libraries to create the game of life with a UI that shows how program evolves over time based on the four rules presented above.

The code is available on this [github repository](https://github.com/franciscomesquitaAI/Learning_Notes/blob/d3747f4cdb7bdafa1689af4e9ec400b65e5bdcd3/Informatic-Related/Techniques-Frameworks-Methods-Tools/Game-Of-Life/Game_Of_Life.ipynb).

Let me show you some example from one of my experiments with random starting values as input:

![game of life example](https://i.imgur.com/X2tdarS.gif)


There are a lot of more interesting patterns that you can look at \[4], \[5] and \[6]. **There is even a competition a competition called "Pattern of the Year (POTY) \[7] **


---

# Experiment it

You can try different initial configurations and see if you can find a cool pattern or you can try already identified interesting patterns. That is available at \[8]

![Game Of Life experiment it](https://i.imgur.com/qKNfBk4.png)


---

# References

\[1]: [https://chalkdustmagazine.com/blog/reproduce-or-die/](https://chalkdustmagazine.com/blog/reproduce-or-die/)

\[2]: [https://www.compadre.org/osp/EJSS/3577/12.htm](https://www.compadre.org/osp/EJSS/3577/12.htm) 

\[3]: [https://www.cs.utexas.edu/~byoung/cs303e/project2-GameOfLife.html](https://www.cs.utexas.edu/~byoung/cs303e/project2-GameOfLife.html)

\[4]: [https://copy.sh/life/examples/](https://copy.sh/life/examples/)

\[5]: [https://playgameoflife.com/](https://playgameoflife.com/)

\[6]: [https://conwaylife.com/](https://conwaylife.com/)

\[7]: [https://conwaylife.com/wiki/Pattern_of_the_Year](https://conwaylife.com/wiki/Pattern_of_the_Year)

\[8]: [https://playgameoflife.com/](https://playgameoflife.com/)
