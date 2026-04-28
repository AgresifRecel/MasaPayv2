import express from "express";
import fetch from "node-fetch";
import cors from "cors";

const app = express();
app.use(cors());

app.get("/menu", async (req, res) => {
  try {
    const response = await fetch(
      "https://europe-west3-paragastroteka-inventory.cloudfunctions.net/getQrMenu?customerId=sakal-kafe-bar&branchId=sakal-kafe-bar-1"
    );

    const data = await response.json();

    const all = [];

    data.categories.forEach((cat) => {
      (cat.sections || []).forEach((sec) => {
        (sec.products || []).forEach((p) => {
          all.push({
            name: p.name,
            price: p.price,
            category: sec.name || cat.name
          });
        });
      });
    });

    res.json(all);
  } catch (err) {
    console.log(err);
    res.status(500).json({ error: "menu alınamadı" });
  }
});

app.listen(10000, () => console.log("server çalışıyor"));
