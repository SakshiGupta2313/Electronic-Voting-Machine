# Electronic Voting Machine (EVM)

## Project Overview

This project is an Arduino-based Electronic Voting Machine developed as part of my Electronics and Communication Engineering studies. It allows users to cast votes using push buttons and displays voting information on an LCD.

## Features

- Voting through push buttons
- 16x2 LCD display
- LED indication after vote registration
- Buzzer feedback
- Vote counting
- Result display
- SD card storage for voting data

## Components Used

- Arduino
- 16x2 LCD with I2C
- Push Buttons
- LED
- Buzzer
- SD Card Module
- Breadboard
- Jumper Wires

## Working

The voter selects a candidate using the corresponding push button. The Arduino registers the vote and provides LED and buzzer feedback. The LCD displays the voting information, and the result button displays the vote count.

## Hardware Connections

- Vote Buttons: D2–D7
- Buzzer: D8
- Result Button: D9
- SD Card CS: D10
- LED: D11
- LCD SDA: A4
- LCD SCL: A5

## Project Structure

- `Arduino_Code` – Arduino program
- `Circuit_Diagram` – Circuit diagram
- `Documentation` – Project documentation
- `Images` – Project images

## Future Enhancements

- Password-protected result access
- Improved user interface
- More secure vote storage
- Additional voting features

## Project Type

ECE Mini Project
