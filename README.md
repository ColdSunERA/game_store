# Game Store Module for Drupal 11

A custom Drupal 11 module for managing in-game item listings with prices in gold and quantities.

## Features

- **Game Item Entity**: Create items with name and image
- **Game Listing Entity**: Create listings that reference multiple items, each with their own price (in gold) and quantity
- **Admin Interface**: Manage items and listings through Drupal's admin interface
- **Views Integration**: Default view at `/listings` to display all game listings
- **Custom Template**: Formatted table display showing items with images, prices, and quantities

## Module Structure

```
game_store/
├── game_store.info.yml
├── game_store.module
├── game_store.permissions.yml
├── game_store.install
├── README.md
├── src/
│   ├── Entity/
│   │   ├── Item.php
│   │   └── Listing.php
│   ├── ItemListBuilder.php
│   └── ListingListBuilder.php
├── templates/
│   └── game-listing.html.twig
└── config/
    └── install/
        └── views.view.game_listings.yml
```

## Installation

1. Place the `game_store` folder in your `modules/custom` directory
2. Enable the module: `drush en game_store -y`
3. Clear cache: `drush cr`

## Usage

### Creating Items

1. Navigate to `/admin/content/game-items`
2. Click "Add Game Item"
3. Enter item name and upload an image
4. Save

### Creating Listings

1. Navigate to `/admin/content/game-listings`
2. Click "Add Game Listing"
3. Enter a title
4. Add items by typing their names (autocomplete)
5. **Important**: Enter prices and quantities in the same order as items
   - First price corresponds to first item
   - Second price corresponds to second item, etc.
6. Save

### Viewing Listings

- Public view: `/listings`
- Admin list: `/admin/content/game-listings`

## Important Notes

### Data Synchronization

The current implementation uses three separate multi-value fields (items, prices, quantities). The relationship between them is maintained by array index position. When adding a listing:

- Item at index 0 → Price at index 0 → Quantity at index 0
- Item at index 1 → Price at index 1 → Quantity at index 1
- And so on...

**Ensure you add the same number of values for items, prices, and quantities.**

## Permissions

- **Administer game items**: Create, edit, delete items
- **Administer game listings**: Create, edit, delete listings
- **View game listings**: View the public listings page

Grant these permissions at `/admin/people/permissions`

## Customization

### Custom Template

The module includes a custom Twig template at `templates/game-listing.html.twig` that displays listings in a table format. Modify this template to change the display.

### View Configuration

The default view can be customized at `/admin/structure/views/view/game_listings`

## Requirements

- Drupal 11
- Core modules: field, image, views

## License

GPL-2.0-or-later
