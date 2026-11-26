# Meme-Driven IDE: Gamifying Developer Workflows via Real-Time Custom Object Detection

An individual project for the McGill MMA course **MGSC673**.

## Overview

Traditional software development involves long hours of repetitive keyboard and mouse interactions, which can lead to developer fatigue, monotony, and repetitive strain injuries (RSI), while debugging and running tests can feel tedious.

This project explores a playful, hands-free **Meme-Driven Interactive Coding Environment** that gamifies developer workflows. Using a standard webcam feed, a custom deep learning object detection model detects and classifies physical "meme cards" (printed popular internet memes) or memes displayed on a smartphone/secondary screen in real time, translating those visual cues into actionable IDE shortcuts and programming commands.

## Meme Templates (`Memes/`)

The repository currently includes **7 meme templates** in [`Memes/`](Memes/):

| File | Meme Name | Also Known As / Origin |
| :--- | :--- | :--- |
| [`black-guy-pointing-at-head.png`](Memes/black-guy-pointing-at-head.png) | **Roll Safe** | Guy Pointing at His Head (Kayode Ewumi in *Hood Documentary*) |
| [`cat.webp`](Memes/cat.webp) | **Woman Yelling at a Cat** | Taylor Armstrong (*RHOBH*) & Smudge the Cat |
| [`clarkson.jpg`](Memes/clarkson.jpg) | **Jeremy Clarkson Driving an Ariel Atom** | *Top Gear* (Series 5, Episode 9) |
| [`eminem.jpeg`](Memes/eminem.jpeg) | **Eminem Throwing Things** | "Woe, Plague Be Upon Ye" (fan-made *GQ* cover mockup) |
| [`red-angry-bird.webp`](Memes/red-angry-bird.webp) | **Angry Bird Ear** | Angry Bird Listening / "I'm All Ears" |
| [`shock.webp`](Memes/shock.webp) | **Disintegrating Emoji** | Screaming Emoji / Emoji Turning to Dust / "NOOOO" Emoji |
| [`shocked-black-guy.jpg`](Memes/shocked-black-guy.jpg) | **Shocked Black Guy** | Surprised Black Guy (YouTuber Jslutty) |

## Example Meme-to-Command Mappings (Proposal)

Illustrative mappings proposed to demonstrate how detected memes can trigger IDE and system actions:

| Meme Template | Triggered Action |
| :--- | :--- |
| **This is Fine** | Force-compile code |
| **Success Kid** | Trigger a test suite |
| **Two Buttons** | Toggle between terminal tabs |
| **Hide the Pain Harold** | Mute the system |

## Dataset

Rather than relying on a public dataset, this project uses a custom, self-annotated dataset designed to match real-world desk-setup webcam detection:

- **Collection:** Captured via a personal laptop webcam with memes printed on paper or displayed on a smartphone across varied orientations, distances, and lighting conditions.
- **Classes:** 5 to 10 popular meme templates (7 templates currently stored in [`Memes/`](Memes/)).
- **Approximate Size:** 15 to 20 annotated images.
- **Input Variables:** RGB image frames (e.g., `640×640` resolution) from the webcam's field of view.
- **Target / Output:** Bounding box coordinates `(x, y, width, height)` and the categorical class label for each meme template present in the frame.

## Deep Learning Approach

- **Architecture & Transfer Learning:** Uses the **YOLO** family of object detection models. Because training a CNN from scratch on a small custom dataset would cause severe overfitting, pre-trained YOLO weights are fine-tuned via transfer learning.
- **Data Augmentation:** Evaluates techniques such as random brightness, blur, and rotation to simulate different office lighting conditions and webcam qualities for robust real-time inference.
- **Evaluation Metrics:** mean Average Precision (**mAP**), Intersection over Union (**IoU**), **precision**, and **recall**.

## Real-Time Application & Tech Stack

Beyond test-set evaluation, the trained model powers a real-time interactive **Python** application:

- **OpenCV:** Processes the live webcam feed.
- **Fine-Tuned YOLO:** Runs real-time object detection inference on incoming frames.
- **PyAutoGUI:** Maps high-confidence meme detections to system-level keyboard shortcuts or IDE commands.

## Inspiration

- [Instagram Reel](https://www.instagram.com/reel/Ddm5NJHvjQU/?rpxt=MTR3NWJjd2htemNpMw==)
