;; handy-mathy-bank
;; handy tools to run math algorithms
;; (okay I admit I made this cuz I'm too lazy to solve them by hand)

;; This file would be written in full Racket.
;; Updated version in Pyhton coming soon.

#lang racket

;; (my-gcd x y) calculates the greatest common denominator of input
;; natural numbers x and y
;; my-gcd: Nat Nat -> Int
;; requires: x >= y;
(define (my-gcd x y)
  (cond
    [(x = 0) y]
    [(y = 0) x]
    [(= (remainder x y) 0) y]
    [else (my-gcd y (remainder x y))]))

;; Tests
(my-gcd 17612 128)
(my-gcd 57 12)


;; (EEA a b) gives the entire EEA table of natural numbers a and b
;; requires a >= b
(define (EEA a b)
  (local 
  [(define (one-row 2ndlast last a b)
    (list (- (first 2ndlast) (* (quotient a b) (first last)))
          (- (second 2ndlast) (* (quotient a b) (second last)))
          (remainder a b)
          (quotient a b)))
    (define (EEA-acc a b acc)
     (cond
       [(= 0 (remainder a b)) acc]
       [else
        (EEA-acc b (remainder a b) 
                 (cons  (one-row (second acc) (first acc) a b) acc))]))]
    (reverse
     (EEA-acc a b (list (list 0 1 b 0)
                        (list 1 0 a 0))))))

;; Tests
(EEA 48 11)
(EEA 57 12)
