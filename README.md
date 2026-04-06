# RockPaperScissors-4
RockPaperScissors.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RockPaperScissors {
    enum Choice { None, Rock, Paper, Scissors }

    mapping(address => Choice) public playerChoice;
    address public player1;
    address public player2;

    function play(Choice _choice) public {
        require(_choice != Choice.None, "Invalid choice");
        if (player1 == address(0)) player1 = msg.sender;
        else if (player2 == address(0)) player2 = msg.sender;

        playerChoice[msg.sender] = _choice;
    }

    function determineWinner() public view returns (string memory) {
        Choice c1 = playerChoice[player1];
        Choice c2 = playerChoice[player2];

        if (c1 == c2) return "Draw";
        if ((c1 == Choice.Rock && c2 == Choice.Scissors) ||
            (c1 == Choice.Paper && c2 == Choice.Rock) ||
            (c1 == Choice.Scissors && c2 == Choice.Paper)) {
            return "Player 1 wins";
        }
        return "Player 2 wins";
    }
}
