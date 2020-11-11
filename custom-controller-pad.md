# Custom pad for computer control

The aim here is to use a gamepad or a custom pad to control development functions such as run, stop, debug, step in, step out, etc

## ControllerMate

Controller mate is a Mac applicaton to map virtually any gamepad/midi input to keyboard and mouse actions, keystrokes, sequences, etc

{% embed url="https://www.orderedbytes.com/controllermate" %}

## JoyToKey

Map controller to keyboard action on windows

{% embed url="https://joytokey.net/en/" %}

## Keypad reading

How to read keypad input using only one analog input.

{% embed url="http://www.technoblogy.com/show?NGM" %}

## Lightblue bean 

Legacy docs

* [http://legacy.punchthrough.com/files/bean/sdk-docs/index.html](http://legacy.punchthrough.com/files/bean/sdk-docs/index.html)
* [https://punchthrough.github.io/bean-docs/](https://punchthrough.github.io/bean-docs/)

### Pinout

![](.gitbook/assets/image.png)

![](.gitbook/assets/image%20%281%29.png)

### Saving energy

{% embed url="https://punchthrough.github.io/bean-docs/guides/features/power-management/" %}

### Troubleshoot

* Install node using nvm and switch to version 6
* force python command to point to python 2.7
* Error: option 'version' clashes with existing property 'version' on Command
  * [https://git.io/JJc0W](https://git.io/JJc0W
    )
  * `which bean` to find the code locatione
  * Before `program.version(pkg.version).option('-v, --version', 'Get SDK version').action(function (options) {` add:

    ```text
    program
      .storeOptionsAsProperties(false)
      .passCommandToAction(false);
    ```

Some working sketches found in: [https://www.hackster.io/glowascii/lightblue-bean-arduino-basics-de7a94\#team](https://www.hackster.io/glowascii/lightblue-bean-arduino-basics-de7a94#team)

## 16 keys keypad

{% embed url="https://www.factoryforward.com/use-matrix-keypad-single-arduino-pin/" %}

{% embed url="https://arduinogetstarted.com/tutorials/arduino-keypad" %}

{% embed url="http://www.avr-asm-tutorial.net/avr\_en/apps/key\_matrix/keypad/resmatrix/resmatrix.html" %}





