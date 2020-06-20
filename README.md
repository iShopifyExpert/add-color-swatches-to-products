# add-color-swatches-to-products

If you want to use the button treatment on a Size option, use this:


{% if product.available and product.variants.size > 1 %}
{% render 'swatch' with 'Size' as swatch %}
{% endif %}
 

If you want to apply the button or swatch treatment to all your product options, use this:


{% if product.available and product.variants.size > 1 %}
{% render 'swatch' for product.options as swatch %}
{% endif %}
 

With this last snippet, the swatch treatment will be applied automatically to any product option that contains the word colour or color in it, while the button treatment will be applied to all other options.

Locate your selectCallback function
The selectCallback function in a Shopify theme updates the state of the Add to cart button and the displayed selling and “compare at” prices when a variant is selected.

 

Still in your product.liquid file, locate this:

 

selectCallback
 

Don't see it? Under the Layouts folder, locate and click the theme.liquid file to open it in the online code editor. In a fair amount of themes, the selectCallback function is located in this file instead of product.liquid.

 

After you have located your selectCallback function, add the following code to the body of the function, either at the top, or bottom:

 

// BEGIN SWATCHES
if (variant) {
  var form = jQuery('#' + selector.domIdPrefix).closest('form');
  for (var i=0,length=variant.options.length; i<length; i++) {
    var radioButton = form.find('.swatch[data-option-index="' + i + '"] :radio[value="' + variant.options[i] +'"]');
    if (radioButton.size()) {
      radioButton.get(0).checked = true;
    }
  }
}
// END SWATCHES
 

If you add it at the top of the body of the function:

 

swatch-01.jpg


If you add it at the bottom of the body of the function:

 

swatch-02.jpg

 

Add code at the bottom of theme.liquid

Still on the Edit HTML/CSS page, under the Layouts heading on the left, locate and click your theme.liquid file to open it in the online code editor.

 

At the bottom of your theme.liquid file, right above your </body> tag, add this code:

 

<script>
jQuery(function() {
  jQuery('.swatch :radio').change(function() {
    var optionIndex = jQuery(this).closest('.swatch').attr('data-option-index');
    var optionValue = jQuery(this).val();
    jQuery(this)
      .closest('form')
      .find('.single-option-selector')
      .eq(optionIndex)
      .val(optionValue)
      .trigger('change');
  });
});
</script>
