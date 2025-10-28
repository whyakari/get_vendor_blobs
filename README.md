# How to Get Vendor Blobs (Bangkk / Fogos)

> **Use the Bangkk zip** â†’ for the *device-specific vendor*  
> **Use the Fogos zip** â†’ for the *common vendor*

---

## 1. Clone and Set Up dumperx

```bash
git clone https://github.com/<author>/dumperx.git
cd dumperx
./setup.sh
```

> If thereâ€™s no `setup.sh`, make sure tools like `lpunpack`, `payload-dumper-go`, or `payload_dumper.py` are installed.

---

## 2. Dump the Fogos Firmware

Inside the `dumperx` folder, run:

```bash
./dumper.sh link_to_fogos
```

Replace `link_to_fogos` with the actual firmware URL (for example, from **Lolinet**).

After extraction is complete, rename the output folder for clarity:

```bash
mv out/fogos_dump fogos_dump
```

---

## 3. Dump the Bangkk Firmware

Run the dumper again, this time for the Bangkk firmware:

```bash
./dumper.sh https://mirrors.lolinet.com/firmware/lenomola/2023/bangkk/official/RETAIL/BANGKK_RETAIL_15_V1TC35H.88-16_subsidy-DEFAULT_regulatory-DEFAULT_cid50_CFC.xml.zip
```

Rename the output directory:

```bash
mv out/bangkk_dump bangkk_dump
```

---

## 4. Generate the Device-Specific Vendor (Bangkk)

Go to your **Bangkk device tree** folder and run:

```bash
./extract-files.py --only-target path/to/bangkk_dump
```

> This command extracts and generates the **Bangkk-specific vendor blobs**.

---

## 5. Generate the Common Vendor (Fogos)

For the **common blobs**, run:

```bash
./extract-files.py --only-common path/to/fogos_dump
```

> This generates the **common vendor blobs**, shared across devices using the same SoC or hardware base.

---

## Final Tip

The correct extraction order is:

1. Extract **device-specific vendor** first (`--only-target`)
2. Then extract **common vendor** (`--only-common`)

This order ensures that `extract-files.py` organizes everything correctly and prevents conflicts between device-specific and shared blobs.

---

That's it! You now have both the device-specific and common vendor blobs ready to integrate into your ROM build tree.
