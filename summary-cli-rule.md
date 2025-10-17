# Summarize and Review

- Get the gitlab mr diff contents from "./diff.patch"
- Check how large the "./diff.patch" file is and read it in appropriately sized chunks

## Command Summarize


- Instead of analyzing the "./diff.patch" file itself, analyze the MR changes and generate a title summarizing the changes.
- Summarize the changes and save them to "./summary.md" and end the conversation
- If the response is repeated more than 5 times, the conversation must be ended
- The summary must be in Korean
- Except for the "./diff.patch" file, summarize only using the information provided in the prompt

## Command Review

- After reviewing the change, save the review results in JSON format to "./review.json" and end the conversation.
- If the response is repeated more than 5 times, the conversation must be ended
- Except for the "./diff.patch" file, Review only using the information provided in the prompt
- The code review results must follow the given JSON format, but the comments in the example should be omitted.
- The "body" field must be written in Korean.
- `position[newLine]` is the diff line number in the `position[newPath]` file related to the review. If there is no relevant line number, use 0.
- **Line number verification required**: Before setting the `newLine` value for each review item, you must verify the following:
  1. Read the actual file content to confirm the line number is accurate
  2. Verify that the line number calculated from diff matches the corresponding line in the actual file
  3. If uncertain, read the actual file directly to find the correct line
- **Review process**:
  1. Analyze the diff.patch file to identify changes
  2. Identify review points for each change
  3. Calculate and verify the accurate line number for review points
  4. Generate review.json with verified line numbers
- Only write items that need improvement, and if there are none, save an empty `[]` JSON file.

### How to Calculate the Review Line Number

**Important: Line number calculation must be accurate. Incorrect line numbers will display reviews in the wrong location.**

#### Step-by-step line number calculation method:

1. **Analyze hunk header**: `@@ -oldStart,oldCount +newStart,newCount @@` where `newStart` is the starting line of the new file
2. **Calculate only changed lines**: Only lines starting with `+` are counted as new file lines
3. **Ignore removed lines**: Lines starting with `-` are not in the new file, so exclude them from calculation
4. **Find exact position**: Determine which `+` line number the code you want to review is in the hunk

#### Example:

```diff
--- packages/ad-player/src/components/log/send-log.ts
+++ packages/ad-player/src/components/log/send-log.ts
@@ -127,7 +127,7 @@ const transformLogType = (type: LogPayload['type']) => {
     case 'ad-error': {
       return 'fail'
     }
-    
-    case 'ad-info-loaded': {
+    case 'ad-roll-info-loaded': {
       return 'request'
     }
     default: {
```

**Calculation process:**
- Hunk header: `@@ -127,7 +127,7 @@` → New file starting line: 127
- Lines in hunk:
  - `    case 'ad-error': {` (existing line, line 128)
  - `      return 'fail'` (existing line, line 129)  
  - `    }` (existing line, line 130)
  - `-    ` (removed line, ignore)
  - `-    case 'ad-info-loaded': {` (removed line, ignore)
  - `+    case 'ad-roll-info-loaded': {` (new line, line 131)
  - `      return 'request'` (existing line, line 132)
  - `    }` (existing line, line 133)

**Result**: `return 'request'` is line 132 in the new file.

#### Additional verification methods:
- Count `+` lines in order from the diff file
- Verify the exact position of each `+` line in the new file
- If uncertain, read the actual file to confirm the line

#### Line number calculation checklist:
1. ✅ Check `newStart` value in hunk header
2. ✅ Calculate only `+` lines in order within the hunk
3. ✅ Ignore `-` lines as they don't exist in the new file
4. ✅ Identify which `+` line number the review target code is
5. ✅ Calculate final line number with `newStart + (order - 1)`
6. ✅ Read the actual file to verify the line number is correct

#### Example verification:
```diff
@@ -127,7 +127,7 @@
     case 'ad-error': {          // existing line (line 128)
       return 'fail'            // existing line (line 129)
     }                          // existing line (line 130)
-                               // removed line (ignore)
-    case 'ad-info-loaded': {   // removed line (ignore)
+    case 'ad-roll-info-loaded': { // new line (line 131)
       return 'request'         // existing line (line 132)
     }                          // existing line (line 133)
```

**Calculation process:**
- Hunk start: 127
- `+    case 'ad-roll-info-loaded': {` is the first `+` line
- Final line number: 127 + 1 = 128 ❌ (incorrect calculation)
- Correct calculation: 127 + 4 = 131 ✅ (3 existing lines + 1 new line)


```JSON
[
  {
    // {string} (required) review message
    "body": "대상에 대한 리뷰 메세지 1",
    "position": {
      // {string} diff old file path from the "./diff.patch" (required)
      "oldPath": "/path/to/file1.js",
      // {string} diff new file path from the "./diff.patch" (required)
      "newPath": "/path/to/file1.js",
      // {number} review target diff line number" (required)
      "newLine": 123
    }
  },
  {
    // {string} (required) review message
    "body": "대상에 대한 리뷰 메세지 2",
    "position": {
      // {string} diff old file path from the "./diff.patch" (required)
      "oldPath": "/path/to/file2.js",
      // {string} diff new file path from the "./diff.patch" (required)
      "newPath": "/path/to/file2.js",
      // {number} review target diff line number" (required)
      "newLine": 30
    }
  }
]
```

## Double Check

- You must create both the summary result file "./summary.md" and the review result file "./review.json".
- **Final line number verification**: Before generating review.json, verify the following:
  1. Reconfirm that each review item's `newLine` value is accurate
  2. Verify that the actual file content matches the diff content
  3. If line number is not 0, ensure there is actual code at that line
  4. Set uncertain line numbers to 0 for whole-file review
