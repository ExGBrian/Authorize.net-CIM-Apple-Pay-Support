# Authorize.Net Apple Pay Universal

A WordPress plugin that adds universal Apple Pay button support with WooCommerce shipping integration for the Authorize.Net payment gateway.

## Features

- ✅ Universal Apple Pay button for cart and checkout pages
- ✅ Full WooCommerce shipping integration
- ✅ CheckoutWC compatibility
- ✅ Real-time shipping calculation
- ✅ Support for virtual and physical products
- ✅ Comprehensive error handling
- ✅ Apple Pay API v3 compliant
- ✅ Shortcode support for custom placements
- ✅ Extensive debugging and logging

## Requirements

- WordPress 5.0 or higher
- WooCommerce 3.0 or higher
- [WooCommerce Authorize.Net Gateway](https://woocommerce.com/products/authorize-net/) plugin (by SkyVerge)
- Valid Apple Pay merchant ID configured in Authorize.Net
- SSL certificate (HTTPS required for Apple Pay)
- Apple device for testing (iPhone, iPad, or Mac with Safari)

## Installation

1. **Upload the plugin**
   - Upload the `authorize-net-apple-pay.php` file to `/wp-content/plugins/authorize-net-apple-pay-universal/`
   - Or install via WordPress admin: Plugins → Add New → Upload Plugin

2. **Activate the plugin**
   - Go to WordPress admin → Plugins
   - Find "Authorize.Net Apple Pay Universal"
   - Click "Activate"

3. **Configure Authorize.Net Gateway**
   - Ensure the WooCommerce Authorize.Net Gateway plugin is installed and activated
   - Go to WooCommerce → Settings → Payments → Authorize.Net
   - Configure your API credentials
   - Enable and configure Apple Pay settings with your merchant ID

4. **Configure WooCommerce Shipping**
   - Go to WooCommerce → Settings → Shipping
   - Set up your shipping zones and methods
   - Ensure shipping methods are available for your target regions

## Usage

### Automatic Display

The Apple Pay button automatically appears on:
- Cart page (above checkout button)
- Checkout page (before customer details)
- CheckoutWC express payment section (if using CheckoutWC)

### Shortcode

Place the Apple Pay button anywhere using:
```
[apple_pay_button]
```

### Customization

The button styling can be customized via CSS:
```css
apple-pay-button.apple-pay-button-universal {
    --apple-pay-button-width: 200px;
    --apple-pay-button-height: 48px;
    --apple-pay-button-border-radius: 5px;
}
```

## How It Works

1. **User clicks Apple Pay button**
   - Payment sheet opens with cart details
   
2. **User selects shipping address**
   - Plugin calculates available shipping methods
   - Displays shipping options in Apple Pay sheet
   
3. **User selects shipping method**
   - Total updates with selected shipping cost
   - Tax recalculated if applicable
   
4. **User authorizes payment**
   - Payment processed through Authorize.Net
   - Order created in WooCommerce
   - User redirected to order confirmation

## Debugging

### Enable WordPress Debug Log

Add to `wp-config.php`:
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

### Check Server Logs

View `/wp-content/debug.log` for entries like:
```
Apple Pay Shipping Request: Array(...)
Apple Pay: Found X shipping methods
Apple Pay: No shipping methods available for address
```

### Browser Console

Open Safari Developer Tools and check console for:
```
Apple Pay: Shipping contact selected
Apple Pay: Shipping response {success: true, ...}
Apple Pay: Found 2 shipping methods
```

## Troubleshooting

### Apple Pay button doesn't appear
- Ensure you're using Safari on a supported Apple device
- Check that SSL/HTTPS is enabled
- Verify Authorize.Net gateway is active and configured
- Confirm Apple Pay is enabled in gateway settings

### Payment sheet aborts when selecting address
- Check server debug log for errors
- Verify shipping zones are configured correctly
- Ensure shipping methods are available for the selected address
- Check browser console for JavaScript errors

### No shipping methods shown
- Verify shipping zones cover the destination
- Check shipping method restrictions (weight, price, etc.)
- Review debug log for "No shipping methods available" message
- Test with different addresses

### Errors during payment
- Verify API credentials in Authorize.Net settings
- Check that merchant ID matches your Apple Pay configuration
- Review WooCommerce order notes for error details
- Check Authorize.Net transaction logs

## Compatibility

### Tested With
- WordPress 5.0+
- WooCommerce 3.0+
- WooCommerce Authorize.Net Gateway 3.10+
- SkyVerge Payment Gateway Framework 5.15+
- CheckoutWC 7.0+

### Browser Support
- Safari on iOS 10+
- Safari on macOS 10.12+
- No support for Chrome, Firefox, or other browsers (Apple Pay limitation)

## Error Handling

The plugin handles various error scenarios:

- **Invalid address data**: Returns error to Apple Pay
- **No shipping methods available**: Shows user-friendly message
- **Virtual products**: Skips shipping requirement
- **Network errors**: Graceful fallback with error message
- **Server errors**: Logged for debugging

## Security

- AJAX requests use WordPress nonces for security
- Address data sanitized before processing
- Follows WordPress coding standards
- No sensitive data stored client-side

## Changelog

### Version 1.3.0
- Fixed Apple Pay sheet abort issue when selecting shipping address
- Added proper error handling with ApplePayError objects
- Updated to Apple Pay API v3 format
- Added comprehensive logging and debugging
- Created shared `build_line_items()` helper method
- Improved handling of virtual products
- Enhanced error messages for better UX

## Support

For issues or questions:
1. Check the Troubleshooting section above
2. Enable debug logging and check logs
3. Review browser console for errors
4. Verify all requirements are met

## License

This plugin is provided as-is without warranty. Use at your own risk.

## Credits

**Author**: Brian Paknoosh
**Built for**: WooCommerce + Authorize.Net Gateway integration  
**Apple Pay**: Apple Inc.  
**Payment Gateway Framework**: SkyVerge
