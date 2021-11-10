# chromeprintbug
Reproduceable Chrome Print Bug

On current version of chrome 95.0.4638.69 (Official Build) (64-bit) - and chromium based products such as Edge - an empty flexbox element with a gap attribue when printing is attmpted will result in the print-preview document believing it is many thousands of pages long freezing/crashing the tab.
If the gap attribute is remove from the stylesheet, the bug no longer occurs.

Also, if the element contains children that are hidden via a print stylesheet to display:none the error still occurs, so I am speculating that the print preview code optimizes by removing display:none elements in their entirety instead of simply hiding them or giving them zero size.

Further speculate that the implementation of gap calculations in the print preview is not checking for child elements and is diving straight into a loop which is now somewhat infinite because the length of child elements is zero instead of an expected positive INT value.


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <style>
        div#test {
            display: flex;
            gap: 1px;
        }
    </style>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id='test'></div>
</body>
<script>window.print();</script>
</html>
