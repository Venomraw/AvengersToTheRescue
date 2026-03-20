# Leek

For this challenge, I will be using Google Chrome, so this may be different if you're using a different browser

# Finding the Flag

It is a lot easier to do this challenge by going to the website itself instead of being in the gym. So click on the arrow on the top right of the website window to go to the website. From there, we will do the following

- Hit F12/Right click and click inspect

    Click on network in the inspect window. (If there are elements there, click the 🚫 symbol to clear them out)

- Add an item

    You can type in whatever you want into the box. When you're done, click add.

- Go back to the inspect window

    There should be an element there called `add`.

- Copy the element

    Right click on element and hover over copy. Then click `Copy URL`.

- Paste the URL in a Bash Terminal (Terminal for Mac)

    Paste the URL in the following command. **The URL must be in quotes**

    ```
    curl '(Insert URL here)' \
    -H 'Accept: */*' \
    -H 'Content-Type: application/json' \
    -H 'sec-ch-ua: "Not_A Brand";v="8", "Chromium";v="120", "Google Chrome";v="120"' \
    --data-raw '{"content":100}' \
    --compressed
    ```

    After you execute the command, refresh the page and the flag should be there.