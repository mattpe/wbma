class: center, middle

# WBMA, Pipes

## 2/2018

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

### Task: Create a _custom_ pipe and use it to get thumbnail images of the media files

1. Use your previous [exercise](w4-upload.md) as a starting point (preferred) or clone teacher's [simplified starter project](https://github.com/wbma/pipe-starter)
1. Use `FrontComponent` to show thumbnails of the 10 newest media files
    - add getNewFiles() method into `MediaService` and use [GET /media](http://media.mw.metropolia.fi/wbma/docs/#api-Media-GetMediaFiles)
    - inject MediaService into your `FrontComponent`
    - use `*ngFor` to list files in component's html template
1. [Check from api docs](http://media.mw.metropolia.fi/wbma/docs/#api-Media-GetFile) how thumbnail files can be accessed
1. Use angular-cli to generate a new pipe called _thumbnail_ into _src/app/pipes_ folder : `ng generate pipes/[PIPE-NAME]` ([Custom pipes @ Angular docs](https://angular.io/guide/pipes#custom-pipes))
1. Edit the `transform()` method in the `thumbnail.pipe.ts` file:
    - it should get a filename in as a parameter (`value`)
    - optional size (options: `large`, `medium`, `small` and `screenshot`) as an args parameter (use one the sizes as a default if not specified in the expression)
    - return the thumbnail's filename of selected size
1. Use the pipe in your _front.component.html_ file, example of usage:

    ```html
    <div *ngFor="let file of mediaFiles">
      <img [alt]="file?.title" [src]="'http://media.mw.metropolia.fi/wbma/uploads/' + (file?.filename | thumbnail: 'small')">
        <!-- should transform: SOMEIMAGE.jpg => SOMEIMAGE-tn160.png -->
    </div>
    ```


  **Why to use thumbnails instead of full size files?**
