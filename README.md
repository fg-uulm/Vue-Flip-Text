# Vue-Flip-Text
A vue.js flip text label component - see demo at http://florian-geiselhart.de

# Purpose
The sole purpose is to animate from random gibberish text to a predefined text in a nice way. The algorithm is based on randomness 
and thus not deterministic in terms of duration. Under certain conditions (e.g. special characters), it might not converge at all.
Please open an issue if this happens.

# Usage
The component exposes following properties:

* text: The text to show in the label
* chance: How high the chance is for a single character to be replaced by the target character during one iteration
* time: Time in milliseconds between iterations
