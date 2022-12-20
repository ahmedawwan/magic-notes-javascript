# magic-notes-javascript

Magic notes web app developed using bootstrap and JavaScript.

You can Add, Search, Delete, Save your notes.

Go have a look at it yourself: [live preview](https://ahmedawwan.github.io/magic-notes-javascript/)

![alt text](https://raw.githubusercontent.com/ahmedawwan/magic-notes-javascript/master/images/Animation.gif?token=GHSAT0AAAAAABTY7V42RA72TJEPYZHBEWNKYTBCYNA)

### Show notes 

```javascript
function showNotes() {
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesObj = [];
    } else {
        notesObj = JSON.parse(notes);
    }

    let html = "";
    notesObj.forEach(function(element, index) {
        html += `
        <div class="noteCard card my-2 mx-2" style="width: 18rem;">
        <div class="card-body">
            <h5 class="card-title">Note ${index + 1}</h5>
            <p class="card-text">${element}</p>
            <button id = ${index} onclick = "deleteNote(this.id)" class="btn btn-danger">Delete Note</button>
        </div>
    </div>
    `
    });
    let notesElm = document.getElementById('notes');
    if (notesObj.length != 0) {
        notesElm.innerHTML = html;
    } else {
        notesElm.innerHTML = `Nothing to show! Please add a note`;
    }
};
```


### Add Notes

Listener on the Add Note button

```javascript
addBtn.addEventListener('click', function(e) {
    // Lets get the textarea in which we wrote our Note
    let addTxt = document.getElementById('addTxt');
    // lets get notes from out local storage (this is in string form)
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesObj = [];
    } else {
        // we created an object notesObj and added all the notes (from our local storage) in it
        notesObj = JSON.parse(notes);
    }
    // we will now add the new note in the notesObj object
    notesObj.push(addTxt.value);
    // we will now stringify the notesObj object and store it in the local storage
    localStorage.setItem("notes", JSON.stringify(notesObj));
    // we'll now clear the text area
    addTxt.value = "";
    showNotes();
});
```

### Delete Note

```javascript
function deleteNote(index) {
    let notes = localStorage.getItem("notes");
    if (notes == null) {
        notesObj = [];
    } else {
        notesObj = JSON.parse(notes);
    }
    notesObj.splice(index, 1);
    localStorage.setItem("notes", JSON.stringify(notesObj));
    showNotes();
    }
```

## Search Notes

Listener on the search text field

```javascript
let search = document.getElementById('searchTxt');
search.addEventListener("input", function() {
    let searchText = search.value.toLowerCase();
    let noteCards = document.getElementsByClassName('noteCard');
    Array.from(noteCards).forEach(function(element) {
        let cardTxt = element.getElementsByTagName("p")[0].innerText.toLowerCase();
        if (cardTxt.includes(searchText)) {
            element.style.display = "block";
        } else {
            element.style.display = "none";
        }
    });
})
```
