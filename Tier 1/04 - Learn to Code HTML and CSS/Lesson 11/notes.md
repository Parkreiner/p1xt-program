# Lesson 11: Organizing Data with Tables

The internet used to be in a really rough place. Before CSS really caught on in almost every browser, developers handled
all their layout through `<table>` elements.

Luckily, CSS allowed style and structure to be separated, and nowadays, tables are only used for their intended purpose:
as tables.

## Creating a table

HTML supplies multiple elements for structuring elaborate and nuanced tables, but in their most simplest form, tables
are just rows and columns.

At the minimum, each HTML table must contain one table row, which itself must contain a piece of table data.

### The `<table>` element

This element indicates the start of a table. This basically serves as a container for all other elements.

### `<tr>` elements

`<tr>` elements are for indicating table rows. HTML does not have elements for indicating columns, so all tables in the
language are row-based. You can have any number of `<tr>` elements in your table.

### `<td>` elements

`<td>` elements are for indicating pieces of table data. These do **not** directly map to cells in the table, as each
piece of data can span multiple columns. However, each `<td>` element will span one unit by default.

### Table headers

The `<th>` element is used to give parts of a table a header. These headers can apply to either to a column or to an
entire row. Functionally, these elements are just like `<td>` elements; in fact, the only main difference is their
semantic meaning.

To define exactly what each `<th>` element applies to, you need to use the `scope` attribute. This attribute takes these
values (with the first two being the most common):

* `col`
* `row`
* `colgroup`
* `rowgroup`

Using `<th>` elements (especially with the `scope`) attribute does wonders to help users who need to use screen readers.

### The `headers` attribute

The `headers` attribute is basically the `scope` attribute, except that it can be applied to any "cell-like" elements
(`<th>` and `<td>`). You can use this when you explicitly want to tie a data element to another `<th>` element. However,
the value of the `headers` attribute for the element you're associating with a `<th>` **must** match the value of that
`<th>` element's `id` attribute.

## Table Structure

So far, we've only covered the basics of tables. A good portion of tables will need no more than a series of rows and
columns, along with a header. However, some will call for a bit more sophistication. This is where elements like
`<caption>`, `<thead>`, `<tbody>`, and `<tfoot>` come in.

### Table captions

The `<caption>` element allows you to provide a table with a caption. It's not to be confused with `<figcaption>`,
which is used exclusively in `<figure>` elements. Whenever you do include a `<caption>` element, it must be the very
first element within the `<table>`, and it certainly can't be nested within any other table elements. In addition, you
can have more than one `<caption>` element inside each `<table>`.

The guide mentions that this element is positioned at the very top of the table by default, making me think that there
are ways to change its position in the webpage without changing its position in the markup.

### Table heads, bodies, and footers

The `<thead>`, `<tbody>`, and `<tfoot>` elements allow you to structure your tables further, breaking them into three
discrete sections: the head, the body, and the footer.

The `<thead>` element is used to contain all content for the table's head. In general, this will mean `<tr>` elements
that contain `<th>` elements. This element does **not** contain the `<caption>` element and instead goes after it.

The `<tbody>` element is for the main content of the table. It's where the bulk of the table data will go.

The `<tfoot>` element, however, is a little interesting. Historically, it needed to immediately follow the `<thead>`
element, but HTML5 is much more lenient, so you can place this element after the `<tbody>` element now. Semantically,
the `<tfoot>` element is for content that describes the structure of the table – it basically acts as an outline.

### Where to place `<thead>`, `<tbody>`, and `<tfoot>` elements

As alluded to earlier, older versions of HTML used to be much more strict about the order you could place the `<thead>`,
`<tbody>`, and `<tfoot>` elements. This was the original order:

1. `<caption>`
2. `<thead>`
3. `<tfoot>`
4. `<tbody>`

As of HTML5, though, you can now place the `<thead>`, `<tbody>`, and `<tfoot>` elements in **any** order, provided that
they aren't nested within each other. However, the `<caption>` element still needs to be the very first element in each
table, so not everything has changed.

Here's an example of all four in action. Note the content put inside the `<tfoot>` element, and how it doesn't directly
map to the content outlined in the `<thead>`:

```html

<table>
    <caption>Design and Front-End Development Books</caption>
    <thead>
    <tr>
        <th scope="col">Item</th>
        <th scope="col">Availability</th>
        <th scope="col">Qty</th>
        <th scope="col">Price</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Don&#8217;t Make Me Think by Steve Krug</td>
        <td>In Stock</td>
        <td>1</td>
        <td>$30.02</td>
    </tr>
    ...
    </tbody>
    <tfoot>
    <tr>
        <td>Subtotal</td>
        <td></td>
        <td></td>
        <td>$135.36</td>
    </tr>
    <tr>
        <td>Tax</td>
        <td></td>
        <td></td>
        <td>$13.54</td>
    </tr>
    <tr>
        <td>Total</td>
        <td></td>
        <td></td>
        <td>$148.90</td>
    </tr>
    </tfoot>
</table>

```

### Combining multiple table cells

Sometimes you need your content to span across multiple cells, either horizontally or vertically. HTML allows you to do
this with the `colspan` and `rowspan` attributes. This is also why it's a good idea not to think of `<td>` and `<th>`
elements being a single cell, as that display tendency can be overridden via CSS.

Just note that when you use the `colspan` attribute, the affected table data element will expand from left to right.
Similarly, `rowspan` expands the table elements it modifies from top to bottom. By using this attribute, you can have
some table rows contain fewer pieces of table data then there are possible cells per row. Just remember that giving an
element the `rowspan` attribute means that the table rows that follow must have fewer than the max number of elements.

Also, at least by default, any content that spans multiple columns and/or rows will be centered both horizontally and
vertically – I'm pretty sure this is how all table cells are.

## Table Borders

Sometimes you're going to want to give your table cells borders. This sections off the content, allowing the reader to
be able to see distinct groups (such as rows) more easily. This helps make the table more intelligible. Luckily, CSS
provides two properties for styling these borders: `border-collapse` and `border-spacing`.

### `border-collapse`

You would think that applying borders to individual rows and columns can be a bit of headache. After all, if each row
has borders on top and bottom, then as the rows stack, their borders will blend together and look way too thick. You
could factor this into the border thickness you give each element, but another, more sensible, solution is to use the
`border-collapse` property. This defines the behavior for what happens when two borders of adjacent elements are right
next to each other. The attribute supports three properties:

* `collapse` - Causes adjacent borders to merge into one
* `separate` - Keeps adjacent borders separate. **This is the default.**
* `inherit` - Inherit the value of the parent element.

Just keep this in mind **because it's one of the most important things when using this property**: you need to apply
the property to the entire table. From my tests, it seems that trying to apply it to individual parts of the table just
doesn't work.

Also, if you try applying borders to `<tr>` table rows without giving the containing `<table>` the `border-collapse`
property, the borders won't display at all. This has something to do with the CSS spec, which I haven't looked up yet.

Interestingly, though, applying the property to a table will remove any of its padding (but not the padding of the
table's content). The reason is that the property merges **all** borders together, meaning that the edges of the cells
are stitched to the edges of the overall table. And because they're stuck together, it's impossible to insert any
padding between them. I don't really get the logic behind this, but it's whatever.

### `border-spacing`

The `border-spacing` property determines how much spacing is given between elements within a table, including their
borders. It's applied to the entire table, and it affects every single thing inside it.

However, the property only works when you give the overall table the `border-collapse:separate` property-value pair.

### Adding borders to rows

As mentioned before, you cannot give borders to `<tr>` elements (at least until you give the table
`border-collapse:collapse`). This can make inserting borders a little tricky at times – you can't just throw a property
on the entire row and call it a day.

Howe just sets the entire table to `border-collapse:collapse` and then gives all `<th>` **and** `<td>` elements padding
and borders. Note that the `<tr>` elements are completely untouched, even though you're aiming to give each row a
border. Then, for a finishing touch, they remove the borders from the very bottom row (which, in this case, is housed
within a `<tfoot>` element).

```css

table {
    border-collapse: collapse;
}

th,
td {
    border-bottom: 1px solid #ddd;
    padding: 10px 15px;
}

/* Functionally identical to `border-bottom: none; */
tfoot tr:last-child td {
    border-bottom: 0;
}

```

### Table Striping

One common thing that designers do for their tables is stripe them. That is, each row in the table alternates in colors,
so that it's obvious which elements belong to which row. You can do this by giving all rows a background color and then
using the `nth-child` selector with a value of `even` or `odd` to change the corresponding rows.

```css
tr {
    background-color: #cecfd5;
}
tr:nth-child(even) {
    background-color: #f0f0f2;
}
```

### Be mindful of borders

Something you need to keep in mind is what happens when you give the main table cells borders but don't do the same to
the `<th>` elements in the table's head. If you have the table set to anything other than `border-collapse: separate`,
the `<td>` elements will be wider, making the table look amateurish.

But since you need to use `border-collapse: separate`, you need to be careful with how you apply your borders. You can't
just give each cell borders on the left and right, because that'll just make them double up in thickness.

### Aligning Text

CSS also lets you determine how text is aligned within each cell, both horizontally and vertically. Unfortunately, it's
not as intuitive as it could be. To change the text's horizontal alignment, you need to use the `text-align` property.
This is the exact same property you use to change the horizontal alignment of all general text elements.

However, to change the text's vertical alignment, you need to use the `vertical-align` property. This property **only**
works within the contexts of tables, which is why vertically centering text was so much of a hassle for so long.
The property accepts a number of values, but the three most common are `top`, `middle`, and `bottom`.

As for when you would use these properties, it's common to align numerical cells flush right. Since the vast majority of
typefaces default to using lining figures, all the numbers should line up. And in general, most designs will also call
for all cell content to be vertically aligned in the middle.