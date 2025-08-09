[Back to README](../README.md)

# Step 1: Blink the Built-in LED

In this step, you'll make the blue LED on your ESP32 board blink on and off.

## What You'll Do
- Write code to turn the built-in LED on and off in a loop

## Instructions

1. Open your `main.py` file in your Pymakr project folder.

2. Copy and paste the following code to get started, and read the explanations below:

    a. **Import the required modules:**
    ```python
    import machine
    import time
    ```
    - `import machine` lets you control the ESP32's hardware (like pins).
    - `import time` lets you pause the program for a set amount of time.

    b. **Set up the LED pin:**
    ```python
    led = machine.Pin(2, machine.Pin.OUT)
    ```
    - This creates a variable called `led` that controls the built-in LED on pin 2.
    - `machine.Pin.OUT` means the pin is used for output (turning the LED on or off).
    - `led.on()` turns the LED on, and `led.off()` turns it off.

    c. **Create a loop to blink the LED:**
    ```python
    while True:
        led.on()
        time.sleep(1)
        led.off()
        time.sleep(1)
    ```
    - `while True:` creates a loop that runs forever.
    - `led.on()` turns the LED on, then `time.sleep(1)` waits for 1 second.
    - `led.off()` turns the LED off, then waits another second.
    - This makes the LED blink on and off every second.

3. Save the file.
4. Click the **Run** button in the Pymakr toolbar to upload and run your code on the ESP32.

## What Should Happen?
- The blue LED on your ESP32 should blink on and off every second.

## Need Help?
- If the LED doesn't blink, check your USB connection and make sure you selected the correct board in Pymakr.
- Ask a classmate or your learning facilitator for help if you're stuck!

---

[Next: Step 2 - Add an External LED](step2.md)
