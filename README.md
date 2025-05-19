# Ex05 Image Carousel
## Date:

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
### APP.JS:

```
import React, { useState } from "react";
import "./App.css";

const images = [
  "Screenshot 2025-05-19 160303.png",
  "Screenshot 2025-05-19 161357.png",
  "https://images.unsplash.com/photo-1462331940025-496dfbfc7564?auto=format&fit=crop&w=800&q=80", 
  "Screenshot 2025-05-19 160623.png", 
  "https://images.unsplash.com/photo-1470770841072-f978cf4d019e?auto=format&fit=crop&w=800&q=80",
];

export default function App() {
  const [current, setCurrent] = useState(2); 

  const prev = () => {
    setCurrent((prev) => (prev === 0 ? images.length - 1 : prev - 1));
  };

  const next = () => {
    setCurrent((prev) => (prev === images.length - 1 ? 0 : prev + 1));
  };

  return (
    <div className="carousel-container">
      <div className="carousel">
        {images.map((src, i) => {
          let className = "slide";

          if (i === current) className += " active";
          else if (i === (current - 1 + images.length) % images.length) className += " left";
          else if (i === (current + 1) % images.length) className += " right";
          else className += " hidden";

          return (
            <img
              key={i}
              src={src}
              alt={`Slide ${i}`}
              className={className}
              draggable={false}
            />
          );
        })}
      </div>
      <div className="buttons">
        <button onClick={prev}>Previous</button>
        <button onClick={next}>Next</button>
      </div>
      <footer>
        <p>2025 SPACE IMAGE CAROUSEL</p>
      </footer>
    </div>
  );
}
```

### APP.CSS:

```
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(90deg, #a7bcff, #c9b8ff);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.carousel-container {
  text-align: center;
}

.carousel {
  position: relative;
  width: 400px;
  height: 300px;
  perspective: 1000px;
  margin: 0 auto 20px;
}

.slide {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 300px;
  height: 220px;
  object-fit: cover;
  border-radius: 10px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.25);
  transform-style: preserve-3d;
  transition: transform 0.5s ease, opacity 0.5s ease;
  opacity: 0;
  transform-origin: center center;
  user-select: none;
  cursor: default;
  filter: drop-shadow(0 5px 10px rgba(0,0,0,0.15));
}

.slide.active {
  opacity: 1;
  transform: translate(-50%, -50%) scale(1.2);
  z-index: 3;
  box-shadow: 0 20px 40px rgba(0,0,0,0.35);
}

.slide.left {
  opacity: 0.8;
  transform: translate(calc(-150% - 20px), -50%) scale(0.8) rotateY(30deg);
  z-index: 2;
}

.slide.right {
  opacity: 0.8;
  transform: translate(calc(50% + 20px), -50%) scale(0.8) rotateY(-30deg);
  z-index: 2;
}

.slide.hidden {
  opacity: 0;
  transform: translate(-50%, -50%) scale(0.5);
  z-index: 1;
  pointer-events: none;
}

.buttons button {
  background-color: #e50039;
  border: none;
  padding: 10px 20px;
  margin: 0 8px;
  color: white;
  font-weight: bold;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 3px 5px rgba(0,0,0,0.2);
  transition: background-color 0.3s ease;
}

.buttons button:hover {
  background-color: #a1032d;
}
footer {
  background-color: rgba(0, 0, 0, 0.1);
  color: #333;
  padding: 10px 0;
  text-align: center;
  width: 100%;
  box-sizing: border-box;
  position: relative; 
  bottom: 0; 
}

footer p {
  margin: 0;
  font-size: 0.9em;
}
```


## OUTPUT

![IMAGE CAROUSEL](https://github.com/user-attachments/assets/0488210c-34c0-41bf-a2da-3e8687604811)


## RESULT
The program for creating Image Carousel using React is executed successfully.
