
# Dropbox Image URL Extractor

This Tampermonkey script allows you to extract image URLs from a Dropbox folder page and copy them to your clipboard with a single click. The script adds a "Copy all URLs" button to the Dropbox page, and when you click the button, it scrolls through the entire folder, collects all image URLs, and copies them to your clipboard.

## Screenshots

Spawns a floating button:

<img width="183" alt="image" src="https://user-images.githubusercontent.com/16804423/235328108-d8626a80-460e-4f30-9c0e-de156ad63897.png">

Click the button and all image URLs are copied to your clipboard

<img width="380" alt="image" src="https://user-images.githubusercontent.com/16804423/235328460-ca13958b-c607-4cc4-802f-17598df1d44a.png">

Paste all your URLs:

<img width="1267" alt="CleanShot 2023-04-29 at 16 40 11@2x" src="https://user-images.githubusercontent.com/16804423/235328423-5da886c8-24bf-4087-a354-5f64b3f52820.png">


## How to Install

1.  Install the Tampermonkey browser extension from the [official website](https://www.tampermonkey.net/).
2.  Open the Tampermonkey dashboard and go to the "Utilities" tab.
3.  Under "URL," paste the raw URL of the script file (e.g., `https://raw.githubusercontent.com/username/repo-name/main/script.js`) and click "Import."
4.  Confirm the installation when prompted.

## How to Use

1.  Navigate to a Dropbox folder page containing images.
2.  Click the "Copy all URLs" button that appears in the bottom right corner of the page.
3.  The script will scroll through the entire folder, collect all image URLs, and copy them to your clipboard.
4.  The button will display the number of URLs copied and will be temporarily disabled for 3 seconds before becoming active again.

## Configuration

You can adjust the `SECONDS_TO_WAIT_FOR_SCROLL` constant in the script to change the amount of time the script waits for new images to load after scrolling to the bottom of the page.

## How it works

The Tampermonkey script is designed to automate the process of extracting image URLs from a Dropbox folder page and copying them to the user's clipboard. The script is executed as a userscript in the context of the browser's web page, and it operates by interacting with the Document Object Model (DOM) of the Dropbox page. Below is a technical explanation of how the script works:

1.  The script starts by defining a set of constants and functions that will be used later in the script:
    
    -   `SECONDS_TO_WAIT_FOR_SCROLL`: A constant that specifies the number of seconds the script should wait for new images to load after scrolling to the bottom of the page.
    -   `DOWNLOAD_URL_REPLACEMENT`: A constant that specifies the query parameter to be appended to the image URLs to enable direct download.
    -   `getImageLinks`: A function that queries the DOM for anchor elements (`<a>`) containing links to image files. It then extracts the `href` attribute of each anchor element, replaces the query parameter `?dl=0` with `?raw=1` to enable direct download, and returns an array of modified URLs.
    -   `waitForImagesToLoad`: An asynchronous function that programmatically scrolls to the bottom of the page and waits for a specified duration (defined by `SECONDS_TO_WAIT_FOR_SCROLL`) to allow new images to load.
2.  The script creates an empty array `imageUrls` to store the image URLs that will be extracted from the page.
    
3.  The script dynamically creates a button element (`<button>`) and appends it to the DOM. The button is styled and positioned in the bottom right corner of the page. The text content of the button is set to "Copy all URLs."
    
4.  The script adds a click event listener to the button. When the button is clicked, the following actions are performed:
    
    -   The script enters a loop that continues until all image URLs have been extracted from the page. The loop is controlled by the `finished` variable, which is initially set to `false`.
    -   Within the loop, the script calls the `waitForImagesToLoad` function to scroll to the bottom of the page and wait for new images to load.
    -   The script then calls the `getImageLinks` function to extract the URLs of the newly loaded images. It filters out any URLs that have already been added to the `imageUrls` array to avoid duplicates.
    -   The script checks whether any new URLs were extracted in the current iteration. If no new URLs were extracted, it sets the `finished` variable to `true`, which will terminate the loop.
    -   The script keeps track of the total number of URLs extracted in the `numUrls` variable.
5.  Once the loop is complete, the script concatenates the image URLs into a single string, separated by newline characters (`\n`), and copies the string to the clipboard using the `GM_setClipboard` function provided by the Tampermonkey API.
    
6.  The script updates the text content of the button to indicate the number of URLs copied to the clipboard and temporarily disables the button for 3 seconds. After this duration, the button is re-enabled, and the text content is reset to "Copy all URLs."
    

The script leverages the Tampermonkey API, DOM manipulation, and asynchronous programming to automate the process of extracting image URLs from a Dropbox folder page and copying them to the user's clipboard. The script is designed to be compatible with the Dropbox web interface.

## License

This project is licensed under the MIT License. See the [LICENSE](https://chat.openai.com/LICENSE) file for details.

## Author

-   Tyler Hall Tech

## Disclaimer

This script is provided "as is" without warranty of any kind. Use it at your own risk. The author is not responsible for any consequences resulting from the use of this script.

----------

As for the URL slug for the GitHub repository, you could use something like `dropbox-image-url-extractor`. This slug is descriptive and clearly indicates the purpose of the repository.`enter code here`
