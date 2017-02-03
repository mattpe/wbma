class: center, middle

# WBMA, Angular Forms + Upload

## 3/2017

---

# Forms

Learn about how Angular handles forms: 

- [Template driven forms](https://blog.thoughtram.io/angular/2016/03/21/template-driven-forms-in-angular-2.html)
- [Model driven forms](https://scotch.io/tutorials/using-angular-2s-model-driven-forms-with-formgroup-and-formcontrol)

### Task: Create Upload Form 

1. Use the previous [exercise](w3-login.md) as a starting point and develop it further
    - or load teachers example from Tuubi (week3t1.zip)
1. Create a new component for the upload functionality
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects) 
    - if you look at login form of teacher's example (week3t1.zip / login.component.*) you can see how the form values are sent with ngSubmit. When sending a file, you also need to include $event (event object)
    - in *.component.ts log event.target to console to find out how to get the input element that has the file
    - create new FormData object, add the file, title and description to the object and send it to the API
    