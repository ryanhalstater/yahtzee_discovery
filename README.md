# Yahtzee Exploration

If you start with five dice and have the option to roll as many dice as you wish, what is the probablility of getting five of the same number within three rolls?
**1.26%**, if you assume the player keeps the dice that are showing the same number.

How we did it (Markov Chain approach):
- Define states: no dice saved, two dice saved, three dice saved, four dice saved, five dice saved
    - We did not include a one die saved because the probability of getting to the other states is the same as in the no-die state
- Solve for the probabilities of transitioning from one state to all other states
    - This yields a transition probability matrix, rows sum up to 1 (like in a Markov Chain)
    - Cells respresent the probability of going from the state represented in the row to the state represented in the column
        - See this image for visual representation: https://d2vlcm61l7u1fs.cloudfront.net/media%2F0bd%2F0bdfd18b-7bb7-406f-b572-b6a45f6e33d8%2FphpYCgbKx.png
- Take this matrix and dot product it with itself twice, and then the probability of getting a Yahtzee within three rolls
   - Uses theoretical result: If you have a transition probability matrix and multiply it by itself n times, it represents the probability of going from row state to column state in n steps

Question: How did we get transition probabilities?
Two different methods yielding the same answer: Combinatorics and Python simulation
- Combinatorics: Compute number of outcomes to get from one state to another, and divide by total number of outcomes
   - Note this required accounting for order (typically through Binomial or Multinomial coefficient) and dividing outcomes into categories 
        - Example: Outcomes going from two dice saved to three dice saved = getting one die of same type and two unique + one same and two different from the first but identical + getting three of same number that was not the original number
        - This computes to: 1\*5*4*BinomialCoeff(3,1) + 1*5*1*BinomCoeff(3,1) + 5
- Simulation: Go through all possible outcomes, count how many go to which state, and divide by the total number of outcomes

Combinatorics: See yahtzee.ods (spreadsheet file openable by LibreOffice or Excel)
Simulation: See Yahtzee.ipynb (Jupyter Notebook file)
