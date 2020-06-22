---
description: Supported HTML tags and CSS properties and selectors
---

# HTML Support

Shotstack supports basic HTML rendering which is useful for styling text and some table based layouts. It is based on a subset of HTML4 and CSS 2.1.

The HTML asset clip can have its [bounding box](https://shotstack.io/docs/api/#tocshtmlasset) size set \(i.e. 400px x 200px\) and can be positioned anywhere on screen using the [position and offset](https://shotstack.io/docs/api/#tocsclip) parameters.

Advanced features of HTML5 such as CSS animations or absolute/relative positioning is not supported at this time. Images are also not currently supported.

### Supported HTML Tags

| Tag | Description | Comment |
| :--- | :--- | :--- |
| `b` | Bold |  |
| `big` | Larger font |  |
| `blockquote` | Indented paragraph |  |
| `body` | Document body | Supports the `bgcolor` attribute, which can be a `#RRGGBB` color specification. |
| `br` | Line break |  |
| `center` | Centered paragraph |  |
| `cite` | Inline citation | Same as `i`. |
| `code` | Code | Same as `tt`. |
| `dd` | Definition data |  |
| `div` | Document division | Supports the standard [block attributes](html-support.md#block-attributes). |
| `dl` | Definition list | Supports the standard [block attributes](html-support.md#block-attributes). |
| `dt` | Definition term | Supports the standard [block attributes](html-support.md#block-attributes). |
| `em` | Emphasized | Same as `i`. |
| `font` | Font size, family, and/or color | Supports the following attributes: `size`, `face`, and `color` \(`#RRGGBB`\). |
| `h1` | Level 1 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `h2` | Level 2 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `h3` | Level 3 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `h4` | Level 4 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `h5` | Level 5 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `h6` | Level 6 heading | Supports the standard [block attributes](html-support.md#block-attributes). |
| `head` | Document header |  |
| `hr` | Horizontal line | Supports the `width` attribute, which can be specified as an absolute or relative \(`%`\) value. |
| `html` | HTML document |  |
| `i` | Italic |  |
| `li` | List item |  |
| `nobr` | Non-breakable text |  |
| `ol` | Ordered list | Supports the standard [list attributes](html-support.md#list-attributes). |
| `p` | Paragraph | Left-aligned by default. Supports the standard [block attributes](html-support.md#block-attributes). |
| `pre` | Preformatted text |  |
| `s` | Strikethrough |  |
| `small` | Small font |  |
| `span` | Grouped elements |  |
| `strong` | Strong | Same as `b`. |
| `sub` | Subscript |  |
| `sup` | Superscript |  |
| `table` | Table | Supports the following attributes: `border`, `bgcolor` \(`#RRGGBB`\), `cellspacing`, `cellpadding`, `width` \(absolute or relative\), and `height`. |
| `tbody` | Table body | Does nothing. |
| `td` | Table data cell | Supports the standard [table cell attributes](html-support.md#table-cell-attributes). |
| `tfoot` | Table footer | Does nothing. |
| `th` | Table header cell | Supports the standard [table cell attributes](html-support.md#table-cell-attributes). |
| `thead` | Table header | If the `thead` tag is specified, it is used when printing tables that span multiple pages. |
| `tr` | Table row | Supports the `bgcolor` attribute, which can be a `#RRGGBB` color specification. |
| `tt` | Typewrite font |  |
| `u` | Underlined |  |
| `ul` | Unordered list | Supports the standard [list attributes](html-support.md#list-attributes). |

#### Block Attributes

The following attributes are supported by the `div`, `dl`, `dt`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `p` tags:

| Attribute | Values |
| :--- | :--- |
| `align` | `left`, `right`, `center`, `justify` |
| `dir` | `ltr`, `rtl` |

#### List Attributes

The following attribute is supported by the `ol` and `ul` tags:

| Attribute | Values |
| :--- | :--- |
| `type` | `1`, `a`, `A`, `square`, `disc`, `circle` |

#### Table Cell Attributes

The following attributes are supported by the `td` and `th` tags:

| Attribute | Values |
| :--- | :--- |
| `width` | Pixel or percentage value |
| `bgcolor` | Hex color value |
| `colspan` |  |
| `rowspan` |  |
| `align` | `left`, `right`, `center`, `justify` |
| `valign` | `top`, `middle`, `bottom` |

### Supported CSS Properties

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Values</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>background-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Background color for elements</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Text foreground color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-family</code>
      </td>
      <td style="text-align:left">&lt;family name&gt;</td>
      <td style="text-align:left">Font family name</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-size</code>
      </td>
      <td style="text-align:left">[ small | medium | large | x-large | xx-large ] | &lt;size&gt;pt | &lt;size&gt;px</td>
      <td
      style="text-align:left">Font size relative to the document font, or specified in points or pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-style</code>
      </td>
      <td style="text-align:left">[ normal | italic | oblique ]</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-weight</code>
      </td>
      <td style="text-align:left">[ normal | bold | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900
        ]</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>text-decoration</code>
      </td>
      <td style="text-align:left">none | [ underline || overline || line-through ]</td>
      <td style="text-align:left">Additional text effects</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font</code>
      </td>
      <td style="text-align:left">[ [ &lt;&apos;font-style&apos;&gt; || &lt;&apos;font-weight&apos;&gt;
        ]? &lt;&apos;font-size&apos;&gt; &lt;&apos;font-family&apos;&gt; ]</td>
      <td
      style="text-align:left">Font shorthand property</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>text-indent</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">First line text indentation in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>white-space</code>
      </td>
      <td style="text-align:left">normal | pre | nowrap | pre-wrap</td>
      <td style="text-align:left">Declares how whitespace in HTML is handled.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>margin-top</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Top paragraph margin in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>margin-bottom</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Bottom paragraph margin in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>margin-left</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Left paragraph margin in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>margin-right</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Right paragraph margin in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>padding-top</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Top table cell padding in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>padding-bottom</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Bottom table cell padding in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>padding-left</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Left table cell padding in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>padding-right</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Right table cell padding in pixels</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>padding</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Shorthand for setting all the padding properties at once.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>vertical-align</code>
      </td>
      <td style="text-align:left">baseline | sub | super | middle | top | bottom</td>
      <td style="text-align:left">Vertical text alignment. For vertical alignment in text table cells only
        middle, top, and bottom apply.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-collapse</code>
      </td>
      <td style="text-align:left">collapse | separate</td>
      <td style="text-align:left">Border Collapse mode for text tables. If set to collapse, cell-spacing
        will not be applied.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Border color for text tables and table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-top-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Top border color for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-bottom-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Bottom border color for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-left-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Left border color for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-right-color</code>
      </td>
      <td style="text-align:left">&lt;color&gt;</td>
      <td style="text-align:left">Right border color for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-style</code>
      </td>
      <td style="text-align:left">none | dotted | dashed | dot-dash | dot-dot-dash | solid | double | groove
        | ridge | inset | outset</td>
      <td style="text-align:left">Border style for text tables and table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-top-style</code>
      </td>
      <td style="text-align:left">&lt;border-style&gt;</td>
      <td style="text-align:left">Top border style for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-bottom-style</code>
      </td>
      <td style="text-align:left">&lt;border-style&gt;</td>
      <td style="text-align:left">Bottom border style for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-left-style</code>
      </td>
      <td style="text-align:left">&lt;border-style&gt;</td>
      <td style="text-align:left">Left border style for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-right-style</code>
      </td>
      <td style="text-align:left">&lt;border-style&gt;</td>
      <td style="text-align:left">Right border style for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-width</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px</td>
      <td style="text-align:left">Width of table or cell border</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-top-width</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Top border width for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-bottom-width</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Bottom border width for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-left-width</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Left border width for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-right-width</code>
      </td>
      <td style="text-align:left">&lt;length&gt;px</td>
      <td style="text-align:left">Right border width for table cells.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-top</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting top border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-bottom</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting bottom border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-left</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting left border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-right</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting right border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-top</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting top border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border-bottom</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting bottom border width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>border</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px &lt;border-style&gt; &lt;border-color&gt;</td>
      <td style="text-align:left">Shorthand for setting all four border&apos;s width, style and color</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>background</code>
      </td>
      <td style="text-align:left">[ &lt;&apos;background-color&apos;&gt; ]</td>
      <td style="text-align:left">Background shorthand property</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>page-break-before</code>
      </td>
      <td style="text-align:left">[ auto | always ]</td>
      <td style="text-align:left">Make it possible to enforce a page break before the paragraph/table</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>page-break-after</code>
      </td>
      <td style="text-align:left">[ auto | always ]</td>
      <td style="text-align:left">Make it possible to enforce a page break after the paragraph/table</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>float</code>
      </td>
      <td style="text-align:left">[ left | right | none ]</td>
      <td style="text-align:left">Specifies where text will be placed in another element. Note that the <code>float</code> property
        is only supported for tables.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>text-transform</code>
      </td>
      <td style="text-align:left">[ uppercase | lowercase ]</td>
      <td style="text-align:left">Select the transformation that will be performed on the text prior to
        displaying it.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-kerning</code>
      </td>
      <td style="text-align:left">[ normal | none ]</td>
      <td style="text-align:left">Enables or disables kerning between text characters.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>font-variant</code>
      </td>
      <td style="text-align:left">small-caps</td>
      <td style="text-align:left">Perform the smallcaps transformation on the text prior to displaying it.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>word-spacing</code>
      </td>
      <td style="text-align:left">&lt;width&gt;px</td>
      <td style="text-align:left">Specifies an alternate spacing between each word.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>line-height</code>
      </td>
      <td style="text-align:left">&lt;number&gt;[% | px | pt | cm]</td>
      <td style="text-align:left">
        <p>Specifies the height of a line. It can be one of the following:</p>
        <ul>
          <li>fixed line height in pixels, points, or centimeters.</li>
          <li>a percentage of the current font size.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Supported CSS Selectors

All CSS 2.1 selector classes are supported except pseudo-class selectors such as :first-child, :visited and :hover.

