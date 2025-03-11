### Steps to Anime List drom Simkl and Save as a File:

#### Step 1: Go to https://simkl.com/{your_id}/anime/
- Replace `{your_id}` with your actual Simkl user ID.
- **For example**, if your Simkl user ID is `6708885`, the URL will look like this:
- https://simkl.com/6708885/anime/

#### Step 2: Open Inspect Mode
- Right-click anywhere on the page and select **Inspect** (or press `Ctrl+Shift+I` on Windows/Linux, or `Cmd+Option+I` on macOS).

#### Step 3: Go to Console
- Navigate to the **Console** tab in the Developer Tools panel.

#### Step 4: Paste the Code Below into the Console
```js
(function() {
    'use strict';

    // Global variable to store the anime titles
    window.animeTitles = [];

    // Select all rows that contain anime information
    const rows = document.querySelectorAll('tr.SimklTVMyTableTR');
    
    rows.forEach((row) => {
        // Find the title within each row
        const titleElement = row.querySelector('.SimklTVMyTableTRTitle a');
        
        if (titleElement) {
            // Extract the title text and push it to the global animeTitles array
            window.animeTitles.push(titleElement.textContent.trim());
        }
    });
    
    // Check if titles were found
    if (window.animeTitles.length > 0) {
        // Print the global variable content to the console
        console.log('Anime Titles:', window.animeTitles);
        
        // Convert the global array to a JSON string
        const jsonContent = JSON.stringify(window.animeTitles, null, 2);

        // Create a data URI for the file
        const dataUri = "data:text/json;charset=utf-8," + encodeURIComponent(jsonContent);

        // Create a link to trigger the download
        const downloadLink = document.createElement('a');
        downloadLink.setAttribute('href', dataUri);
        downloadLink.setAttribute('download', 'watch_list.csv');
        
        // Trigger the download by clicking the link
        downloadLink.click();
    } else {
        console.log('No anime titles found.');
    }
})();
```
#### Step 5: Click Save or Save As to Save the List
- After running the script, a file named **`watch_list.csv`** will be automatically downloaded to your computer.
- If the download doesn't start automatically, right-click the link that appears and choose **Save As** or **Save** to store the file.

