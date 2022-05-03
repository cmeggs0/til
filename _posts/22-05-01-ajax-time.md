# Time to AJAX
The time has come to add dynamic elements to my current project

## jQuery

- Incredibly powerful JavaScript library that makes writing js far easier for your website
- It's by far the most popular js library
- Allows for:
  - HTML/DOM manipulation
  - CSS manipulation
  - HTML event methods
  - Effects and animations
  - AJAX
  - Utilities
- Call method through jQuery() or $()

## AJAX

- The built-in browser developer tools are now my best friend
### Steps to AJAX
1. Break the link
    - Helper methods to bypass breaking the link manually:
      - link_to(remote: true)
      - form_with(local: false)
2. Add format.js to relevant action in controller
3. Create JS response template
4. Find or add unique ids to the html element that you are going to grab onto
    - Think about which template is being rendered, look through forml to see if there are partials, then use html inspect to find the particular element that you need to grab
    - .append and .prepend add children to the selected element
    - .before and .after add siblings
    - Use the console to see where the element will be added
    - escape_javascript or j() is another helper method to avoid the quirks associated with js strings
    - dom_id is another helper method:
```js
comment_<%= comment.id %> == <%= dom_id(comment) %>
```
5. Write jQuery to select element in the DOM
6. Use partials to render with appropriate CSS elements
```js
$("#<%= dom_id(@comment.photo) %>_comment_form").before(`<%= escape_javascript(render("comments/comment", comment: @comment)) %>`);
```
