class: center, middle

# WBMA, Pipes

## 3/2019

---

## Pipe

- takes the output of an expression and transforms it to something else
- pipe operator is `|` (vertical bar)
- multiple pipe operations can be chained

### Example usage with built-in pipes

Value of a `Date` object is passed to DatePipe and the output of that is passed to UpperCasePipe.

`{{ deadlineDate | date:'fullDate' | uppercase }}` outputs: "FRIDAY, FEBRUARY 2, 2018"

 (Fri Feb 02 2018 10:59:26 GMT+0200 (FLE Standard Time) **=>** Friday, February 2, 2018 **=>** FRIDAY, FEBRUARY 2, 2018)

**Read:** [Pipes angular.io guide](https://angular.io/docs/ts/latest/guide/pipes.html).

### Task A: Create a _custom_ pipe and use it to get thumbnail images of the media files

1. Continue last exercise. Create a new branch with git.
1. Show the dates of images in 'HomePage', show the date in Finnish format by using DatePipe. 
1. Use ionic-cli to generate a new pipe called _thumbnail_: `ionic generate pipe [PIPE-NAME]` ([Custom pipes @ Angular docs](https://angular.io/guide/pipes#custom-pipes))
1. Add 'PipesModule' to imports in 'app.module.ts'
1. Modify 'picArray' and 'getAllMedia' method in 'HomePage': 
    ```typescript
    ...
    picArray: Observable<Pic[]>;
    ...
    getAllFiles() {
        this.picArray = this.mediaProvider.getAllMedia();
      }
    ```
1. In home.html add async pipe to *ngFor
1. Edit the `transform()` method in the `pipes/thumbnail/thumbnail.ts` file:
    - it should get file_id in as a parameter (`value`)
    - optional size (options: `large`, `medium`, `small` and `screenshot`) as an args parameter (use one the sizes as a default if not specified in the expression)
    - get the thumbnail filenames from the MediaAPI
    - return the thumbnail's filename of selected size
    - This can be done with [Impure pipe](https://angular.io/guide/pipes#the-impure-asyncpipe) or return a promise from pipe and chain it with async pipe.
1. Use the pipe in your _home.html_ file, example of usage:

    ```html
    <div *ngFor="let file of mediaFiles">
      <img [alt]="file.title" [src]="'http://media.mw.metropolia.fi/wbma/uploads/' + (file.file_id | thumbnail: 'small')">
        <!-- should transform: SOMEIMAGE.jpg => SOMEIMAGE-tn160.png -->
    </div>
    ```

  **Why to use thumbnails instead of full size files?**
  
### Task B: Convert logout page to profile page
1. Change the name of the files and component form logout->profile
1. Add avatar image to the user
    - Use postman to upload image and add a tag 'profile' to it
1. Display users avatar image, name and email in profile page
    - You'll need to add more methods to 'MediaProvider' to achieve this
1. Add logout button to profile page.

