# WooCommerce Order Notice Display Without My Account Page Content

```
// Display order note and status on order details page
function display_order_note_and_status() {
    // Get the current order ID
    $order_id = get_query_var('view-order');

    // Get the order object
    $order = wc_get_order($order_id);

    // Check if the order exists
    if ($order) {
        // Get order number with background color, padding, font weight, line height, display property, and font size
        $order_number = '<span style="font-weight: 600; color: black; background-color: #f7f7f7; padding: 5px 8px; line-height: 1; display: inline-block; font-size: 110%;">' . $order->get_order_number() . '</span>';

        // Get order date with background color, padding, font weight, line height, display property, and font size
        $order_date = $order->get_date_created();
        $formatted_date = '<span style="font-weight: 600; color: black; background-color: #f7f7f7; padding: 5px 8px; line-height: 1; display: inline-block; font-size: 110%;">' . $order_date->date_i18n( get_option( 'date_format' ) ) . '</span>';

        // Get order status with background color, padding, font weight, line height, display property, and font size
        $order_status = $order->get_status();
        $order_status = str_replace('-', ' ', $order_status); // Replace hyphens with a space
        $order_status = '<span style="font-weight: 600; color: black; background-color: #f7f7f7; padding: 5px 8px; line-height: 1; display: inline-block; font-size: 110%;">' . ucfirst($order_status) . '</span>';
        
        // Display order information with custom styles
        echo '<p>Order # ' . $order_number . ' was placed on ' . $formatted_date . ' and is currently ' . $order_status . '.</p>';

        // Display order note
        $order_note = $order->get_customer_note();
        if (!empty($order_note)) {
            echo '<p><strong>' . __('Order Note:', 'woocommerce') . '</strong><br>' . wp_kses_post($order_note) . '</p>';
        }
    }
}
add_action('woocommerce_order_details_before_order_table', 'display_order_note_and_status');

```
