# vuedc_intro01

This code started out as being the solutions to the exercises given during the Introduction to Vue meetups put on by the VueDC Meetup group in October and November 2020. I devitated from the exercises somewhat and built my own functionality, by making the app a full CRUD (Create Read Update Delete) that let me read the To Do list, add new tasks to it, update those tasks, and delete them. Once I got all of that working to my satisfaction, I decided to post it here. 

I am hoping to get constructive feedback on what I've done so that I can do better on my next projects. I'm also offering it as as example that "gets the job done". I'm sure it could be done better but I think it might be useful to someone who wants a "quick and dirty" model CRUD app created in Vue. I'd like to think it is quite clear and simple to understand. 

The parent/root component is in **App.vue**. It calls a **Title** componennt, passing it the information it is supposed to display in the header via props. (I'm envisioning an "all-purpose" header which might serve a variety of related businesses that share the same style but might have different names and proprietors while all being under the same ownership, like a chain of newspapers.) The **Title** component in turn invokes component **DateTimeLocalized** to display the localized Date, Time or both. I see **DateTimeLocalized** as being an example of the kind of component that might be shared by all or most of the code in a codebase, although it's obviously a pretty trivial one. 
The other main component that **App.vue** calls is **ToDoList**, which displays the To Do list and provides buttons that enable new tasks to be created and existing tasks to be updated or deleted. 

When the user presses one of the buttons, the appropriate form for creating, updating or deleting a task is displayed in the right half of the page. That form can be removed by pressing its *Cancel* button, which aborts the attempted Create,Update or Delete, and then hides the form. The other option is that the user can press the other action button on the form, namely *Create Task*, *Update Task* or *Delete Task*. In the case of the *Create Task* and *Update Task* forms, basic edits are done to ensure valid values in the fields, namely that they can't be left blank. (Additional edits could easily be envisioned.) In the event of errors, appropriate messages are displayed and must be fixed before the Create or Update will work. If there are no errors, the task will be created or updated, as the case may be. In the case of the *Delete Task* form, the current information for the task will be displayed greyed out; there are no edits since this is just a confirmation that the user wants that specific data removed. In any case, after the Create, Add or Delete has completed, the form will disappear and the To Do list will be revised and redisplayed. 

The data being displayed in the To Do list originates in **App.vue** and never goes beyond the app. That means that the user can restore the original data by simply refreshing the page. 

## Form Management
I decided to use the **formToShow** field and *v-if* statements to control which form, if any, was visible at any given time. This field is initialized to blank which always ensures that no form is initially displayed. 

Whenever the *Add* button is clicked - there is only one *Add* button - **formToShow** is set to display the Create Task form. If the user presses *Cancel* on the Create Task form, the Create is aborted and the form disappears. If the user presses *Create Task* on the Create form and the data is valid, the new row is emitted to **App.vue**, which adds the row to the Todos array, and the Create form disappears.

If any of the *Update* buttons are clicked, the TaskID for the task on that row of the table is passed to the Task Update form and its data is displayed in editable fields. If the user presses *Cancel* on the Update form, the update is aborted and the form disappears. If the user presses *Update Task* on the Update form and the data is valid, the modified row is emitted to **App.vue**, which updates the Todos array, and the Update form disappears. 

If any of the *Delete* buttons are clicked, the TaskID for the task on that row of the table is passed to the Task Delete form and its data is displayed but can't be edited. If the user presses *Cancel* on the Delete form, the delete is aborted and the form disappears. If the user presses *Delete Task* on the Delete form, the TaskID of the row is emitted to **App.vue**, which removes the row from the Todos array, and the Delete form disappears.   

## Possible Improvements
1. A "real" app would most likely get its information from a database and update that database as the user creates, updates and deletes. I hope to make a new version of this app that includes that functionality in the near future, probably via Laravel. 
2. The app would look slicker if it used Vuetify or something similar. 
3. The editing of the app would look slicker if it used Vuelidate or something similar.
4. Having the two sides of the page (below the date) in scrollable windows would make the app much better capable to handle data that has more rows and/or columns. Alternatively, the ToDoList should use the entire width of the page and then be replaced by **TaskCreate**, **TaskUpdate**, or **TaskDelete** as appropriate when one of the buttons on **ToDoList** is pressed. 
5. A component that lets users create, update or delete the data directly within the table rather than in a separate form would let the To Do list have the whole width of the screen to work with. I'm picturing something where each cell of the table is clickable so that you could change it (assuming your change passed edits) or a row could be deleted by clicking a *Delete Task* button. New tasks would involve clicking a button to create a new empty row which would also be edited to make sure it was entirely valid. That would allow the **ToDoList** to be the full width of the screen eliminate the need for the forms altogether since the functionality would be added directly to the **ToDoList**. 

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```

npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
