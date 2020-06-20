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
