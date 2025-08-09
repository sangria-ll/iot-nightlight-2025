[Back to README](../README.md) | [Previous: Step 5](step5.md)

# Step 6 (Bonus): Choose Your Own Upgrade!

In this bonus step, pick one of two activities to make your nightlight even smarter. Each activity is a real-world skill used in IoT (Internet of Things) devices!

## Activity 1: Change the Threshold from the Web Page

Have you ever set up a smart device and adjusted its settings from your phone or computer? In this activity, you'll add a feature to your nightlight's web page so you can change the light threshold (the value that decides when the light turns on) without editing code!

**What You'll Do:**
- Add a form to your web page to set the threshold value
- Update your code to read the new threshold from the web

**Why?**
- This is just like adjusting the brightness or sensitivity of a real IoT device from its app or web dashboard.

[See instructions for Activity 1](#activity-1-instructions)

---

## Activity 2: Live Updates with AJAX (Advanced)

Want to make your web page update instantly as the sensor value changes, without refreshing? In this activity, you'll use AJAX polling—a technology used by many smart home dashboards and IoT devices for live updates.

**What You'll Do:**
- Change your ESP32 code to serve a web page that uses AJAX polling
- Send live sensor and LED status updates to the browser every second
- (Optional) Let the browser send commands back to the ESP32

**Why?**
- This is how many IoT dashboards and smart home apps show live data!

[See instructions for Activity 2](#activity-2-instructions)

---

## Activity 1 Instructions

1. Open your [`main.py`](../my_nightlight/main.py).
2. Add a form to your `web_page` function to set the threshold value (see previous steps for code examples).
3. Update your request handling code to parse the threshold value from the URL and update the `threshold` variable.
4. Save and upload your code, then use the web page to set the threshold!

---

## Activity 2 Instructions (Advanced)

1. Update your ESP32 code to serve a web page with a JavaScript function that uses AJAX (XMLHttpRequest or fetch) to request status updates from a `/status` endpoint every second.
2. In your main loop, respond to `/status` requests with a JSON object containing the sensor, LED, mode, and threshold values.
3. Update your web page JavaScript to receive and display live updates in the browser.
4. (Optional) Add controls to the web page to send commands back to the ESP32.

---

🎉 Pick the activity that excites you most and make your nightlight even smarter!

---

[Back to README](../README.md) | [Previous: Step 5](step5.md)
