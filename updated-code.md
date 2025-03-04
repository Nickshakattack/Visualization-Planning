class BarGraph {
  constructor(data, x, y, w, h) {
    this.data = data;
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.margin = 50;
    this.barWidth = (this.w - 2 * this.margin) / this.data.length - 10;
    this.maxValue = max(this.data.map(d => d.snowDepth));
  }

  draw() {
    for (let i = 0; i < this.data.length; i++) {
      let barHeight = map(this.data[i].snowDepth, 0, this.maxValue, 0, this.h - 100);
      let barX = this.x + this.margin + i * (this.barWidth + 20);
      let barY = this.y + this.h - barHeight - this.margin;

      // Hover effect
      if (mouseX > barX && mouseX < barX + this.barWidth && mouseY > barY) {
        fill(255, 100, 100);
        textSize(16);
        textAlign(CENTER);
        text(`${this.data[i].month}: ${this.data[i].snowDepth} inches`, mouseX, mouseY - 20);
      } else {
        fill(0, 102, 204);
      }

      // Draw bar
      rect(barX, barY, this.barWidth, barHeight);

      // Draw month labels
      fill(0);
      textSize(14);
      textAlign(CENTER);
      text(this.data[i].month, barX + this.barWidth / 2, this.y + this.h - this.margin + 20);
    }
  }

  sortData() {
    this.data.sort((a, b) => b.snowDepth - a.snowDepth);
  }
}

// Sample snow depth data
let snowData = [
  { month: "Jan", snowDepth: 10 },
  { month: "Feb", snowDepth: 12 },
  { month: "Mar", snowDepth: 8 },
  { month: "Apr", snowDepth: 5 },
  { month: "May", snowDepth: 1 },
  { month: "Jun", snowDepth: 0 },
  { month: "Jul", snowDepth: 0 },
  { month: "Aug", snowDepth: 0 },
  { month: "Sep", snowDepth: 0 },
  { month: "Oct", snowDepth: 2 },
  { month: "Nov", snowDepth: 6 },
  { month: "Dec", snowDepth: 9 }
];

let graph;
let button;

function setup() {
  createCanvas(1000, 600);
  graph = new BarGraph(snowData, 50, 50, 900, 500);

  button = createButton("Sort by Snow Depth");
  button.position(10, 10);
  button.mousePressed(() => {
    graph.sortData();
  });
}

function draw() {
  background(240);
  graph.draw();
}
