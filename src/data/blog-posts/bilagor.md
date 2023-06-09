---
title: 6.Bilagor
publishDate: 1 Jun 2023
description: Various sources
---

## Bilagor

<div class="container">

Här följer bifogade bilagor.

<br />

## Github länk

Github-kontot tillhör Bidstacker och delas endast internt.

<br />

## Rules for Widgets

```md
## Widget

11 variables per widget as of now, all are optional except for id and title(optional should be marked as undefined)

-  id: number
-  title: string
-  type: string
-  style: string
-  width: string
-  buttonStyle: string
-  buttonType: string
-  buttonDesc: string
-  dropdownOptions: string[]
-  buttonAction: function
-  content: JSX.Element

## Widget Types

-  requestor
-  supplier
-  carrier

## Widget Styles

Are the styles that the widget loads with, can not be changed by the user as of now

-  CARDS_FORM_STYLE[0] = 'bg-white px-4 py-6 rounded-xl h-full'
-  CARDS_FORM_STYLE[1] = 'bg-white px-4 py-5 rounded-xl h-full'
-  CARDS_FORM_STYLE[2] = 'bg-white px-4 py-3 rounded-xl h-full'
-  CARDS_FORM_STYLE[3] = 'bg-gradient-to-b from-white to-blue-600 px-4 py-3 rounded-xl h-full'

## Widget Widths

Are the width that an widget loads with, can be changed by the user

-  w-full
-  w-1/2

## Widget Button Styles

Are the styles that the widget button loads with, can not be changed by the user as of now

## Widget Button Types

Are the types that define what the button does, as of now only the following are available

-  dropdown
-  addProjectItem

## Widget Button Descriptions

Are the descriptions that the primary widget button loads with

-  'Nytt projekt' for example

## Widget Dropdown Options

Are the options that the dropdown widget button loads with

-  ['Kvartalsrapport', 'Månadsrapport', 'Översikt'] for example

## Widget Button Actions

Are the actions that the widget button does when clicked, as of now only the following are available

-  dropdownHandler
-  addProjectItemHandler

## Widget Content

Is the content that the widget loads with. Should be a JSX.Element from the Widgets folder with needed props.

Data is loaded from the backend and passed as props to the content component.
```

## User Stories

**Inköpare:**

1. User should be able to see the number of created requests, received offers, waiting for approval and received orders
2. User could overview the quarterly report, monthly report and overview of of various information
3. User should be able to add and, delete and handle projects
4. User should be able to see the weather
5. User should be able to see the latest contacts

**Supplier:**

1. User should be able to see the number of active offers, sent offers, received orders and delivered orders
2. User could overview the quarterly report, monthly report and overview of of various information
3. User should be able to see the weather
4. User should be able to see the latest contacts

**Bud:**

1. User should be able to see the number of active offers, sent offers, received orders and delivered orders
2. User could overview the quarterly report, monthly report and overview of of various information
3. User should be able to see the weather
4. User should be able to see the latest contacts

## Bilder

<br />

  </div>

<style>
  .start {
    margin-top: 1em;
  }
  .abstract-image {
    float: right;
    margin: -1em 1em 2em 2em;
    max-width: 400px;
  }

  .abstract-image img {
    border-radius: 8px;
    margin-bottom: 1.5em;
  }

  @media (max-width: 1020px) {
    .abstract-image {
      float: none;
      margin: 0 auto 2em;
    }
  }
</style>
