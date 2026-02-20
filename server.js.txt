const express = require("express");
const fetch = require("node-fetch");
const app = express();

const API_KEY = process.env.NdfKJ5o4RaqokSlEleOYcw==; // stored securely in Railway

app.get("/bus-arrivals", async (req, res) => {
  const stopId = req.query.stopId;
  try {
    const response = await fetch(`https://datamall2.mytransport.sg/ltaodataservice/v3/BusArrival?BusStopCode=${stopId}`, {
      headers: {
        "AccountKey": API_KEY,
        "accept": "application/json"
      }
    });
    const data = await response.json();
    res.setHeader("Access-Control-Allow-Origin", "*");
    res.json(data);
  } catch (err) {
    res.status(500).json({ error: "Failed to fetch bus data" });
  }
});

const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Proxy running on port ${port}`));




