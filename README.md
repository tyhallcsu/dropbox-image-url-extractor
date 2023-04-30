
# Dropbox Image URL Extractor

This Tampermonkey script allows you to extract image URLs from a Dropbox folder page and copy them to your clipboard with a single click. The script adds a "Copy all URLs" button to the Dropbox page, and when you click the button, it scrolls through the entire folder, collects all image URLs, and copies them to your clipboard.

This is a userscript that extracts image URLs from a Dropbox page and copies them to the clipboard when a button is clicked. The script creates a button on the page that, when clicked, scrolls to the bottom of the page, waits for new images to load, and extracts the image URLs. The script then joins the URLs into a string separated by newlines. It then puts the links on your clipboard with ?dl=0 replaced with ?raw=1 parameters.

## Bulk Extract All Dropbox Image URLs in Shared Folder to Clipboard

> The power of extracting image URLs from a Dropbox folder page and copying them to your clipboard with a single click!

## Screenshots

Floating button in the bottom right of your browser window:

<img width="183" alt="image" src="https://user-images.githubusercontent.com/16804423/235328108-d8626a80-460e-4f30-9c0e-de156ad63897.png">

Click the button and all image URLs are copied to your clipboard

<img width="380" alt="image" src="https://user-images.githubusercontent.com/16804423/235328460-ca13958b-c607-4cc4-802f-17598df1d44a.png">

Paste all your URLs:

<img width="1267" alt="CleanShot 2023-04-29 at 16 40 11@2x" src="https://user-images.githubusercontent.com/16804423/235328423-5da886c8-24bf-4087-a354-5f64b3f52820.png">


## How to Install

1.  Install the Tampermonkey browser extension from the [official website](https://www.tampermonkey.net/).
2.  Open the Tampermonkey dashboard and go to the "Utilities" tab.
3.  Under "URL," paste the raw URL of the script file (e.g., `https://raw.githubusercontent.com/tyhallcsu/dropbox-image-url-extractor/main/dropbox-image-bulk-url-extractor`) and click "Import."
4.  Confirm the installation when prompted.

## How to Use

1.  Navigate to a Dropbox folder page containing images.
2.  Click the "Copy all URLs" button that appears in the bottom right corner of the page.
3.  The script will scroll through the entire folder, collect all image URLs, and copy them to your clipboard.
4.  The button will display the number of URLs copied and will be temporarily disabled for 3 seconds before becoming active again.

## About

> [Changelog (GitHub)](https://github.com/tyhallcsu/dropbox-image-url-extractor/releases)

This Tampermonkey script allows you to extract image URLs from a Dropbox folder page and copy them to your clipboard with a single click. The script adds a "Copy all URLs" button to the Dropbox page, and when you click the button, it scrolls through the entire folder, collects all image URLs, and copies them to your clipboard.

**Known bugs:**

-   None.

## Preview(s)

<img width="500" alt="Preview" src="https://user-images.githubusercontent.com/16804423/235327792-5bd222eb-5be0-485c-afc8-026daf1fe726.png">

## Downloads

----------

***

| Version | Link | Alternative | Note |
|:----------:|:----------:|:----------:|:----------:|
Userscript | [Greasy Fork](https://greasyfork.org/scripts/866731) | [Install (GitHub)](https://github.com/tyhallcsu/dropbox-image-url-extractor/releases/latest/download/dropbox-image-url-extractor) | Work in Progress
Chrome/Edge/Opera | [GitHub](https://github.com/tyhallcsu/dropbox-image-url-extractor/releases) | - | Work in progress
Legacy | [Gist](https://gist.github.com/tyhallcsu/89d6c672f93e94cbd651354b587306b4) | [Link](https://www.dropboxforum.com/t5/View-download-and-export/Export-Bulk-Dropbox-Image-Folder-URLs/td-p/677302) | -


**(Optional) Mobile Bookmarklet:**

JSCopy code

`javascript:(function(){['https://raw.githubusercontent.com/tyhallcsu/dropbox-image-url-extractor/main/dropbox-image-bulk-url-extractor'].map(s=>document.body.appendChild(document.createElement('script')).src=s)})();` 

----------

## Features

> Tested and compatible with Tampermonkey.

-   Automatically scrolls through the entire Dropbox folder to load all images.
-   Extracts image URLs and copies them to the clipboard with a single click.
-   Button is temporarily disabled after copying URLs to prevent accidental clicks.
-   Configurable wait time for loading new images.

## FAQ / Troubleshooting

Nothing appears bottom right:

-   Try again on another Dropbox folder page.
-   Make sure the Tampermonkey extension is enabled and the script is installed.
-   If issue persists, see [Viewing UserJS Logs](https://github.com/tyhallcsu/dropbox-image-url-extractor/#viewing-userjs-logs).

## Viewing UserJS Logs

-   Open your web browser's Inspect Element and navigate to its Console.
-   Locate the following **[UserScript] < message >** (you can filter your Console by entering **UserScript** or **[**).
-   Feel free to screenshot any error messages to the [GitHub](https://github.com/tyhallcsu/dropbox-image-url-extractor/issues) for additional help.
-   If nothing appears, this means the script is not executing at all.

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

### Source Code

-   [https://github.com/tyhallcsu/dropbox-image-url-extractor](https://github.com/tyhallcsu/dropbox-image-url-extractor)

### Contacts

[GitHub](https://github.com/tyhallcsu)

[Twitter](https://twitter.com/sharmanhall)

[Greasy Fork](https://greasyfork.org/en/users/866731)

[Sleazy Fork](https://sleazyfork.org/en/users/866731)

[OpenJS](https://www.openjs.com/scripts/)

[Open UserJS:](https://openuserjs.org/users/sharmanhall/scripts)

[Gist (GitHub):](https://gist.github.com/tyhallcsu/89d6c672f93e94cbd651354b587306b4)

[Dropbox](https://www.dropboxforum.com/t5/View-download-and-export/Export-Bulk-Dropbox-Image-Folder-URLs/td-p/677302)

Tyler Hall Tech

## Disclaimer

This script is provided "as is" without warranty of any kind. Use it at your own risk. The author is not responsible for any consequences resulting from the use of this script.

----------

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/tyhallcsu/dropbox-image-url-extractor/blob/main/LICENSE) file for details.

## Author

-   Tyler Hall Tech
