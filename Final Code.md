// Sample data: Average snow depth in inches for each month
let snowData = [
  { month: "January", snowDepth: 10 },
  { month: "February", snowDepth: 12 },
  { month: "March", snowDepth: 8 },
  { month: "April", snowDepth: 5 },
  { month: "May", snowDepth: 1 },
  { month: "June", snowDepth: 0 },
  { month: "July", snowDepth: 0 },
  { month: "August", snowDepth: 0 },
  { month: "September", snowDepth: 0 },
  { month: "October", snowDepth: 2 },
  { month: "November", snowDepth: 6 },
  { month: "December", snowDepth: 9 }
];

function setup() {
  createCanvas(800, 400);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(220);
  let barWidth = width / snowData.length;

  for (let i = 0; i < snowData.length; i++) {
    let barHeight = map(snowData[i].snowDepth, 0, 15, 0, height - 50);
    let x = i * barWidth;
    let y = height - barHeight;

    // Check if mouse is over the bar
   if (mouseX > x && mouseX < x + barWidth && mouseY > y) {
      fill(100, 150, 255);
      // Display tooltip
      textSize(16);
      text(
     `${snowData[i].month}: ${snowData[i].snowDepth} inches`,
        mouseX,
        mouseY - 20
      );
    } else {
      fill(100, 100, 255);
    }

    // Draw bar
  rect(x, y, barWidth - 10, barHeight);

    // Draw month label
  fill(0);
   textSize(12);
    text(snowData[i].month, x + barWidth / 2, height - 10);
  }
}
