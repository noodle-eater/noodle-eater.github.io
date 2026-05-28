---
title: "Coding Quest — Automating Spellchecking for Unreal Engine 5 Localization"
excerpt: >-
  A small experiment automating spellchecking on Unreal Engine 5 localization
  files using Python — exporting .po files, running pyspellchecker, and writing
  the corrections back so smaller teams can catch typos without a dedicated
  proofreader.
date: 2025-01-01
tags: ["unreal-engine", "python", "automation"]
header:
  teaser: /assets/images/posts/coding-quest-ue5-spellcheck/ue5-localization-dashboard.png
---

It's been a while since I last wrote on Medium, and I'm eager to start sharing again — whether it's about something I'm learning or experiments I want to try. More than that, I've been thinking about doing something like a coding adventure, inspired by [Sebastian Lague](https://www.youtube.com/@SebastianLague) and his awesome [YouTube channel](https://www.youtube.com/@SebastianLague). I find his projects cool and motivating, and I'd love to explore similar paths. In this article, I'll walk you through a small experiment I did: automating spellchecking in Unreal Engine 5 localization files using Python.

## A. Introduction

In game development, text plays a crucial role — whether it's in menus, dialogue, or tutorials. As the game grows, so does the amount of text, increasing the chances of typos. While hiring professionals for localization and proofreading is ideal, it may not be feasible for smaller studios. Fortunately, we can automate typo checks to save costs without compromising quality.

Unreal Engine's localization system allows easy export of text files for external processing. By using Python, we can automate spellchecking on these files. Python is a popular tool for automation and supports Unreal scripting, making it ideal for this task. Additionally, Python's rich set of libraries for natural language processing enhances spellchecking in the localization pipeline.

This guide focuses on **English (en)** text, but the process can be adapted for other languages.

![Unreal Engine 5 Localization Dashboard](/assets/images/posts/coding-quest-ue5-spellcheck/ue5-localization-dashboard.png)

## B. Implementation

### a. Setting Up Python for Unreal Engine 5

Before diving into the spellchecking script, we first need to set up Python. I use **PyCharm** and **Python 3.11.8**, and rely on Python's virtual environment (venv) to manage project dependencies and keep the plugin libraries separate.

To set up Python in Unreal Engine, follow the [Scripting the Unreal Editor Using Python](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python) guide. This will help configure Unreal to recognize your Python installation.

After setting up, export your localization files from Unreal Engine in the **.po** format. This format is commonly used in software localization and will be the target file for spellchecking. Once exported, you can access and manipulate the **.po** files using Python.

### b. Installing Required Libraries

To perform spellchecking and handle the .po files, we'll need two Python libraries:

- **pyspellchecker**: A lightweight library for spell checking.
- **polib**: A library specifically designed for handling `.po` and `.mo` files used in software localization.

You can install these libraries in two ways:

**Using pip in terminal**

```bash
pip install pyspellchecker polib
```

**Using PyCharm**

- Open your project in PyCharm.
- Go to **File > Settings > Project > Python Interpreter**.
- Click the **+** icon to add a new library.
- Search for **pyspellchecker** and **polib**, and click **Install** for each.

### c. Challenges Encountered

While working on the spellchecking script, I encountered a few issues:

- **Unreal's Isolated Python Environment**: By default, Unreal Engine has an isolated Python environment, meaning it can't access libraries or virtual environments outside the engine itself.
- **sys.path.append Attempt**: Initially, I tried using `sys.path.append` to add my virtual environment to Unreal's Python library path, but this approach stopped working for reasons I couldn't pinpoint.
- **Solution**: I eventually added my Python environment directly through Unreal Engine's settings. Go to **Project Settings > Plugins > Python**, and under the Python section, add the environment you want to use. This allowed Unreal to access the necessary libraries and plugins.

![Unreal Engine 5 — Python Additional Path](/assets/images/posts/coding-quest-ue5-spellcheck/ue5-python-additional-path.png)

### d. Running the Script

You can run the script directly from PyCharm or within Unreal Engine by navigating to **Tools > Execute Python Script**.

In the Python script, we only process the **msgstr** fields, as these contain translatable text that we can modify. The **msgid** fields, on the other hand, are used internally to link the source content with its corresponding translation and should remain unchanged. Below is the output result of the script, showing how the spellchecker identifies and suggests corrections for misspelled translation text.

```
Misspelled words in entry 'Your majesty's trust in you continues to grow.': {'grow.'}
Suggestions for 'grow.': grows, grown, grow, growl
Misspelled words in entry 'Helllo World!': {'helllo', 'world!'}
Suggestions for 'helllo': hello
Suggestions for 'world!': world, worlds
Misspelled words in entry 'Hello World!': {'world!'}
Suggestions for 'world!': world, worlds
Misspelled words in entry 'Hello Wrold Again!': {'wrold', 'again!'}
Suggestions for 'wrold': world, wold
Suggestions for 'again!': again
Corrected translations saved to D:/UE/UE_Tutorial/Content/Localization/Game/en/Game_Correct.po
```

The **pyspellchecker** library identifies misspelled words and provides a list of suggestions ranked by their similarity to the original word. In this script, we either select the first suggestion, which is often the most likely correction, or implement logic to choose the suggestion with the highest similarity. This ensures that errors are corrected efficiently while maintaining accuracy in the localized text.

## C. Future Expansion

To enhance the script, we can integrate it into the Unreal Engine build pipeline, automating spellchecking with each build. Alternatively, we could add a GUI to present spellcheck suggestions, allowing users to select corrections or manually input custom words, offering more flexibility for edge cases or game-specific terms.

---

Thank you for reading till the end! I hope this guide was helpful or sparked some new ideas for your own projects. Have a great day!

*Originally published on [Medium](https://noodle-eater.medium.com/coding-quest-automating-spellchecking-for-unreal-engine-5-localization-bbcd5bc07c66).*
