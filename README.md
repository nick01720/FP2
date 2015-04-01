# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)

This is just like FP1, but where you do a different library. (Full description of FP1 is [on Piazza.][piazza])

During this assignment, you should start looking for teammates. See the project schedule [on Piazza.][schedule]

Write your report right in this file. Instructions are below. You can delete them if you like, or just leave them at the bottom.
You are allowed to change/delete anything in this file to make it into your report. It will be public.

This file is formatted with the [**markdown** language][markdown], so take a glance at how that works.

This file IS your report for the assignment, including code and your story.

Code is super easy in markdown, which you can easily do inline `(require net/url)` or do in whole blocks:
```
#lang racket

(require net/url)
```

### My Library: pict library

I found the pict library which works with things that racket can output in the console from text to images. I went through the different sections of the library sampling some of the different things it was capable of doing. (For intesive purposes any "shape" is a picture of the library) I started with outputting shapes, filling in shapes, connecting shapes, combining shapes, making tables of numbers, rotating shapes, bordering shapes, choosing the color of a shape, changing the opaqueness of a shape. There are also different images from the library that i outputted including: clouds, fish, jack-o'-lanterns, angel wings, a devil racket computer, thermometer, a fish with a speech bubble, a (large) happy face, and flash borders (like in comic books). One of the more interesting aspects was that the library has procedures that accept code and output it. The colors and format of the code can also be changed. A fun aspect is that it has a tree layout sub-library that will output trees in different formats. The binary-tidier process produces some cool looking trees. The library also has a pict converter sub-library that will take certaing structures turn them into pics. A miscellaneous process will output a picture as a hyperling, blue and underlined. Overall following the basic code and playing around with the library helped me find out more about what racket had to offer, such as the color database which is pretty sizeable.

```
#lang racket

(require pict)

(blank 50)

(text "Nicholas Forsyth")
(text "g & t" (cons 'bold 'roman))
(text "martini" null 13 (/ pi 2))

(hline 40 5)
(vline 5 40 #:segment 5)

(frame (circle 30))

(frame (circle 30) #:segment 5)

(frame (circle 30) #:color "chartreuse" #:line-width 3)

(ellipse 40 30)

(circle 30)

(filled-ellipse 30 40)

(disk 30)

(rectangle 50 50)

(filled-rectangle 50 80)

(rounded-rectangle 40 40 -0.3 #:angle (/ pi 4))

(filled-rounded-rectangle 50 40)

(arrow 30 0)

(arrow 30 (/ pi 2))

(arrowhead 30 0)

(bitmap (arrowhead 30 0))

;(pip-line 10 10 10)

;(pip-arrow-line 10 10 10)

;(pip-arrows-line 10 10 10)

(define pict-a (rectangle 40 40))
 
(define pict-b (circle 40))
 
(define combined (hc-append 200 pict-a pict-b))
 
(pin-line combined
            pict-a cc-find
            pict-b cc-find)

(pin-arrow-line 30 combined
                  pict-a rc-find
                  pict-b lc-find
                  #:line-width 3
                  #:style 'long-dash
                  #:color "medium goldenrod")

(pin-arrows-line 30 combined
                   pict-a rc-find
                   pict-b lc-find
                   #:start-angle (/ pi 11)
                   #:end-angle (- (/ pi 11))
                   #:solid? #f)

(define combiners (list vl-append vc-append vr-append
                        ht-append htl-append hc-append
                        hbl-append hb-append))
 
(define names (list "vl-append" "vc-append" "vr-append"
                    "ht-append" "htl-append" "hc-append"
                    "hbl-append" "hb-append"))
 
(define pict-a2 (colorize (filled-rectangle 60 30) "tomato"))
 
(define pict-b2 (colorize (disk 45) "cornflower blue"))
 
(define picts
  (for/list ([combiner combiners] [name names])
    (list (text name null 15)
          (combiner pict-a2 pict-b2))))

(take picts 4)

(define combiners2 (list lt-superimpose  ltl-superimpose lc-superimpose
                        lbl-superimpose lb-superimpose  ct-superimpose
                        ctl-superimpose cc-superimpose  cbl-superimpose
                        cb-superimpose  rt-superimpose  rtl-superimpose
                        rc-superimpose  rbl-superimpose rb-superimpose))
 
(define names2 (list "lt-superimpose"  "ltl-superimpose" "lc-superimpose"
                    "lbl-superimpose" "lb-superimpose"  "ct-superimpose"
                    "ctl-superimpose" "cc-superimpose"  "cbl-superimpose"
                    "cb-superimpose"  "rt-superimpose"  "rtl-superimpose"
                    "rc-superimpose"  "rbl-superimpose" "rb-superimpose"))
 
(define pict-a3 (colorize (filled-rectangle 60 30) "tomato"))
 
(define pict-b3 (colorize (disk 45) "cornflower blue"))
 
(define picts2
  (for/list ([combiner combiners2] [name names2])
    (list (text name null 15)
          (combiner pict-a3 pict-b3))))

(take picts2 3)

(take (drop picts2 3) 3)

(take (drop picts2 6) 3)

(take (drop picts2 9) 3)

(take (drop picts2 12) 3)

(table 4
         (map (λ (x) (text (format "~a" x)))
              (list 1 2 3 4
                    5 6 7 8
                    9000 10 11 12))
         cc-superimpose
         cc-superimpose
         10
         10)

(table 4
         (map (λ (x) (text (format "~a" x)))
              (list 1 2 3 4
                    5 6 7 8
                    9000 10 11 12))
         rc-superimpose
         cc-superimpose
         10
         10)

(filled-rectangle 80 40)

;(scale (filled-rectangle 40 20) 2)

;(scale (filled-rectangle 20 20) 4 2)

(rotate (filled-rectangle 80 40) (/ pi 2))

(ghost (filled-rectangle 80 40))

;(ghost (rotate (filled-rectangle 80 40) (/ pi 2)))

(linewidth 'long-dash (rotate (rectangle 80 40) (/ pi 2)))

(cellophane (colorize (filled-rectangle 50 50) "MidnightBlue") .5)

(cloud 100 75)

(cloud 100 75 "lavenderblush")

(file-icon 50 60 "bisque")

(file-icon 50 60 "honeydew" #t)

(standard-fish 100 50)

(standard-fish 100 50 #:direction 'right #:color "chocolate")

(standard-fish 100 50 #:eye-color "saddlebrown" #:color "salmon")

(standard-fish 100 50 #:open-mouth #t #:color "olive")

(jack-o-lantern 100)

(jack-o-lantern 100 "cadet blue" "khaki")

(angel-wing 100 40 #f)

(angel-wing 100 40 #t)

(desktop-machine 1)

(desktop-machine 1 '(devil plt))

(desktop-machine 1 '(plt binary))

(thermometer #:stem-height 90
               #:bottom-circle-diameter 40
               #:top-circle-diameter 20
               #:mercury-inset 4)

(require pict/balloon)

;(balloon-enable-3d #t)

(define a-pict4 (standard-fish 70 40))

(pin-balloon (balloon 40 30 5 'se 5 5)
               (cc-superimpose (blank 300 150) a-pict4)
               a-pict4
               lc-find)

(pin-balloon (wrap-balloon (text "Very fishy") 'sw -5 3)
               (cc-superimpose (blank 300 150) a-pict4)
               a-pict4
               rt-find)

(require pict/face)

(face* 'normal 'huge #f default-face-color 0 -3)

(require pict/flash)

(filled-flash 100 50)

(filled-flash 100 50 8 0.25 (/ pi 2))

(outline-flash 100 50)

(outline-flash 100 50 8 0.25 (/ pi 2))

(require pict/code)

(current-keyword-color "Sienna")

(current-id-color "Goldenrod")

(current-literal-color "DarkKhaki")

(current-base-color "DarkOrange")

(code (lambda (x) (Racket packages are fun)))

(code (+ 1 2))

(code (+ 1 #,(+ 1 1)))

(code (+ 1 #,(frame (code 2))))

(define-syntax two (make-code-transformer #'(code 2)))

(code (+ 1 two))

(current-keyword-color "MidnightBlue")


(let-syntax ([bag (make-code-transformer #'(code hat))]
               [copy (make-code-transformer (syntax-rules ()
                                             [(_ c) (code (* 2 c))]))])
    (inset (frame (code ((copy cat) in the bag))) 2))

;from package pict-lib

(require pict/tree-layout)

(naive-layered (tree-layout
                  (tree-edge #:edge-width 3 (tree-layout))
                  (tree-edge #:edge-color "green" (tree-layout))))

(define (complete d)
    (cond
      [(zero? d) #f]
      [else (define s (complete (- d 1)))
            (tree-layout s s)]))

(naive-layered (complete 4))

(binary-tidier (complete 4))

(define (dl t) (tree-layout (tree-layout #f #f) t))

(define (dr t) (tree-layout t (tree-layout #f #f)))

(binary-tidier
   (tree-layout
    (dr (dr (dr (dl (dl (dl (complete 2)))))))
    (dl (dl (dl (dr (dr (dr (complete 2)))))))))

(hv-alternating (complete 8))

(hyperlinkize (circle 20))

(require pict/convert)

;will turn structures to pics
(pict-convert (circle 20))

```
Output:

![image](https://cloud.githubusercontent.com/assets/7563723/6933438/73f89ea0-d7f5-11e4-9724-9096e0d0c9d2.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933442/820cb594-d7f5-11e4-96fa-742b6bef0cc4.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933445/864cc8ec-d7f5-11e4-80f8-cc9e9ecb38ae.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933447/8abe9144-d7f5-11e4-9116-77f42e5977ae.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933448/8d9aa11e-d7f5-11e4-894a-a34639cc4d7f.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933449/918a57b0-d7f5-11e4-9aba-f13a5ad52771.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933450/94d61008-d7f5-11e4-9070-fcd26d9a2666.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933451/979b6194-d7f5-11e4-84ea-6911e0265d19.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933452/99e0b382-d7f5-11e4-8ed3-53db2b525fc6.png)
![image](https://cloud.githubusercontent.com/assets/7563723/6933454/9d5ab2b0-d7f5-11e4-82ed-ea7d1389c26b.png)


### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request

