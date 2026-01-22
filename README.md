# Simple-contact-app
**350-character project description:**  A beginner-friendly full stack contact application built using HTML, CSS, JavaScript, Node.js, It allows users to add and view contact details through a simple interface. The backend handles REST APIs and stores data in a JSON file, demonstrating basic CRUD operations and client-server communication.
const express = require("express");
const fs = require("fs");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

const PORT = 5000;

// GET data
app.get("/contacts", (req, res) => {
  const data = JSON.parse(fs.readFileSync("backend/data.json"));
  res.json(data);
});

// POST data
app.post("/contacts", (req, res) => {
  const data = JSON.parse(fs.readFileSync("backend/data.json"));
  data.push(req.body);
  fs.writeFileSync("backend/data.json", JSON.stringify(data, null, 2));
  res.json({ message: "Contact saved" });
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
