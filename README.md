# NINL Dhamra SAP Entry Builder

This repository contains a client-side web application designed to automate the creation of SAP entry spreadsheets. It takes Railway Receipt (RR) PDFs as input, parses the text data, and outputs a formatted `.xlsx` file. The tool handles the DPCB to NINS workflow.

## 🚀 Features

*   **Drag-and-Drop Interface:** Easily drop multiple RR PDF files into the designated dropzone or click to browse your local files.
*   **Automated Data Extraction:** Extracts critical information such as RR No, Date, FNR, Commodity Description, Gross Freight, GST, and Weight details (Gross and Net) directly from the PDF.
*   **Grade Matching Engine:** Automatically identifies the material type (COAL or FLUX) and specific material numbers by matching filenames and commodity descriptions against a built-in grade reference table.
*   **Live Preview:** Offers a real-time data table preview of the parsed files before you download the spreadsheet.
*   **Error and Warning Handling:** Flags unparseable files or unrecognized material grades in a dedicated warning box, prompting the user for manual verification.

---

## 📊 Output Structure

The exported `.xlsx` file is structured to streamline SAP data entry. The tool organizes the data by dedicating one column per rake.

### Auto-filled Data (Rows 1–16)
These rows are automatically populated using the extracted PDF data and the internal lookup tables.

*   Rake
*   Product
*   Material Nos
*   Storage
*   Date
*   Dispatch plant
*   RR nos (Pre-pended with 'L')
*   FNR Nos
*   Gross
*   Net
*   Gross Freight
*   GST
*   Handling Charges

### Embedded Excel Formulas
Instead of hardcoding all values, the generated spreadsheet uses standard Excel formulas for calculated fields:
*   **Tare:** Calculated as `Gross - Net`.
*   **Net Freight:** Calculated as `Gross Freight - GST`.
*   **Freight Rate:** Calculated as `Net Freight / Net`.

### Manual Entry (Rows 17–21)
Rows 17 through 21 are intentionally left blank for manual entry by the user. These include:
*   STO nos
*   Delivery
*   Invoice no
*   E-waybill Nos

---

## 🛠️ Technical Details

This tool is built as a single, standalone HTML file with embedded CSS and JavaScript. It relies on the following external libraries delivered via CDN:

*   **PDF Parsing:** `pdf.js` (v3.11.174) is used to read and extract text strings from the uploaded PDFs locally in the browser.
*   **Excel Generation:** `xlsx.full.min.js` (SheetJS v0.18.5) is utilized to format the extracted data into a valid `.xlsx` workbook and trigger the file download.
