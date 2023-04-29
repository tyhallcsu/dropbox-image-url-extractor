
# Dropbox Image URL Extractor

This Tampermonkey script allows you to extract image URLs from a Dropbox folder page and copy them to your clipboard with a single click. The script adds a "Copy all URLs" button to the Dropbox page, and when you click the button, it scrolls through the entire folder, collects all image URLs, and copies them to your clipboard.

## Screenshots

Spawns a floating button:
![CleanShot 2023-04-29 at 16 00 42@2x](https://user-images.githubusercontent.com/16804423/235327792-5bd222eb-5be0-485c-afc8-026daf1fe726.png)

Click the button and all image URLs are copied to your clipboard
![CleanShot 2023-04-29 at 16 00 42@2x2](https://user-images.githubusercontent.com/16804423/235327794-e0dbe1db-e8a3-49f0-9278-736d8a41e8cd.png)


## How to Install

1.  Install the Tampermonkey browser extension from the [official website](https://www.tampermonkey.net/).
2.  Open the Tampermonkey dashboard and go to the "Utilities" tab.
3.  Under "URL," past![Uploading CleanShot 2023-04-29 at 16.00.42@2x.png…]()
e the raw URL of the script file (e.g., `https://raw.githubusercontent.com/username/repo-name/main/script.js`) and click "Import."
4.  Confirm the installation when prompted.

## How to Use

1.  Navigate to a Dropbox folder page containing images.
2.  Click the "Copy all URLs" button that appears in the bottom right corner of the page.
3.  The script will scroll through the entire folder, collect all image URLs, and copy them to your clipboard.
4.  The button will display the number of URLs copied and will be temporarily disabled for 3 seconds before becoming active again.

## Configuration

You can adjust the `SECONDS_TO_WAIT_FOR_SCROLL` constant in the script to change the amount of time the script waits for new images to load after scrolling to the bottom of the page.

## License

This project is licensed under the MIT License. See the [LICENSE](https://chat.openai.com/LICENSE) file for details.

## Author

-   Tyler Hall Tech

## Disclaimer

This script is provided "as is" without warranty of any kind. Use it at your own risk. The author is not responsible for any consequences resulting from the use of this script.

----------

As for the URL slug for the GitHub repository, you could use something like `dropbox-image-url-extractor`. This slug is descriptive and clearly indicates the purpose of the repository.`enter code here`
