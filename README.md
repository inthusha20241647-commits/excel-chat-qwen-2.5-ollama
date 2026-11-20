# Excel Chat with Qwen 2.5 (Ollama + Node.js)

A terminal app that lets you ask questions about an Excel sales sheet in plain English. It runs fully locally using Ollama and the Qwen 2.5 3B model, so no API key is needed and your data never leaves your machine.

> **Status:** experiment, not for production. Verify any figure against the source spreadsheet.

Also see the [Llama 3.2 version](https://github.com/inthusha20241647-commits/excel-chat-ollama) of this project.

## How It Works
1. Reads `sales.xlsx` using the `xlsx` library.
2. Converts the first sheet to CSV.
3. Sends the data and your question to a local model through Ollama's `/api/chat` endpoint (`temperature: 0`).
4. Prints the answer and repeats until you type `exit`.

A strict system prompt tells the model to answer only from the data and to say so when a question can't be answered from the available columns.

## Requirements
![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=nodedotjs&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-installed%20%26%20running-000000?logo=ollama&logoColor=white)
![Model](https://img.shields.io/badge/Model-qwen2.5%3A3b-615CED)

Pull the model:

    ollama pull qwen2.5:3b

## Setup
    git clone https://github.com/inthusha20241647-commits/YOUR-QWEN-REPO-NAME.git
    cd YOUR-QWEN-REPO-NAME
    npm install
    node index.js

- `package.json` must include `"type": "module"`.
- Place your own `sales.xlsx` in the project folder (test columns: Name, Sales, Region, Month).
- Don't commit spreadsheets containing private data.

## Example Questions
- **Direct lookup:** "What is the sale amount for John?"
- **Filtering:** "List all sales in the North region"
- **Calculation:** "What is the total sales amount?"
- **Unanswerable:** "What is John's home address?"

## Findings
Tested on a small sheet (N rows). Each question was run a few times; results are indicative, not statistically rigorous.

| Question type | Result |
|---|---|
| Direct lookup | ✅ Accurate |
| Filtering and listing | ⚠️ Missed items |
| Calculations | ⚠️ Inconsistent |
| Unanswerable | ✅ Said the data can't answer it |

## Limitations
- Small models can make mistakes on sums, averages, and counts.
- Large sheets may exceed the model's context window.

## Future Improvements
- Compute totals and averages in JavaScript and let the model explain results
- Support multiple sheets
- Compare Qwen 2.5 7B and other larger models

## Note
`sales.xlsx` here is sample data only.
