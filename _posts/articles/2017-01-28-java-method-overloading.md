---
layout: post
title: Java Method Overloading Policy
categories: articles
excerpt:
tags: [java, overload]
image:
  feature:
comments: true
share: true
modified: 2016-05-31T16:49:47+09:00
---

# Issue
  문제가 되었던 것은 바로 ElasticSearch QueryBuilder이다. 

# Overloading

## Step1. Without boxing or unboxing
First phase performs overload resolution without permitting boxing or unboxing conversion
먼저 변수의 auto boxing/unboxing 없이 overload를 수행한다.

## Step2. With boxing or unboxing
Second phase performs overload resolution while allowing boxing and unboxing
Step1에서 찾을 수 없

## Step3. variable arity methods + boxing + unboxing
Third phase allows overloading to be combined with variable arity methods, boxing, and unboxing. 

## Step4. Otherwise
If no applicable method is found during these phases, then ambiguity occurs.
