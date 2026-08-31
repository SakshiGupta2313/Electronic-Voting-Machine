# EVM Project Documentation

## Project Overview
This project is an Electronic Voting Machine (EVM) mini project developed as part of Electronics and Communication Engineering studies.

## Components Used
- Arduino
- 16x2 LCD (I2C)
- Push Buttons
- LED
- Buzzer
- SD Card Module

## Working
The voter selects a candidate using the push buttons.
The Arduino processes the selected vote and displays the information on the LCD.
An LED and buzzer provide feedback when a vote is registered.
The result button is used to display the voting results.

## Arduino Pin Connections
- Vote Buttons: D2-D7
- Buzzer: D8
- Result Button: D9
- SD Card CS: D10
- LED: D11
- LCD SDA: A4
- LCD SCL: A5
- SD MOSI: D11
- SD MISO: D12
- SD SCK: D13
