# Skill: browser-automation

This skill documents how to use the OpenClaw-managed browser properly for automation and research tasks.

## 1. Starting the Browser

To start the browser with the OpenClaw profile:

```bash
openclaw browser --browser-profile openclaw start
```

## 2. Navigating to a URL

To navigate to a specific URL:

```bash
openclaw browser --browser-profile openclaw open <url>
```
Replace `<url>` with the desired web address.

## 3. Getting Page Content using JavaScript Evaluation

To evaluate JavaScript that extracts the inner text of the page:

```bash
openclaw browser --browser-profile openclaw eval "document.body.innerText"
```

This outputs the entire text content of the page.

## 4. Saving the Output

Save the output to a file:

```bash
openclaw browser --browser-profile openclaw eval "document.body.innerText" > ~/workspace/page_content.txt
```

## 5. Reading and Extracting

Read the saved file and extract information as needed.

This approach avoids snapshots and directly retrieves page text content via evaluated JavaScript.