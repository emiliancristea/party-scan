# Comprehensive API Documentation Guide

## Current Project Status

This workspace is currently set up for static content deployment to GitHub Pages but does not yet contain source code. This documentation guide provides a framework for comprehensive API documentation once development begins.

## Documentation Framework Overview

This guide covers best practices for documenting:
- **Public APIs** - REST APIs, GraphQL endpoints, SDK methods
- **Functions** - Standalone functions, utility methods, business logic
- **Components** - UI components, modules, classes, services

## Table of Contents

1. [General Documentation Principles](#general-documentation-principles)
2. [API Documentation](#api-documentation)
3. [Function Documentation](#function-documentation)
4. [Component Documentation](#component-documentation)
5. [Language-Specific Guidelines](#language-specific-guidelines)
6. [Documentation Tools and Automation](#documentation-tools-and-automation)
7. [Examples by Framework](#examples-by-framework)

## General Documentation Principles

### Essential Elements for All Documentation

1. **Clear Purpose Statement** - What does this do?
2. **Parameters/Arguments** - What inputs are required/optional?
3. **Return Values** - What outputs are produced?
4. **Usage Examples** - How to use it in practice?
5. **Error Handling** - What can go wrong and how to handle it?
6. **Dependencies** - What external requirements exist?

### Documentation Structure Template

```markdown
## [Function/API/Component Name]

### Description
Brief description of what this does and why it's useful.

### Syntax
```language
// Code signature
```

### Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| param1    | type | Yes      | Description | -       |
| param2    | type | No       | Description | value   |

### Returns
Description of return value and type.

### Examples
```language
// Basic usage example
```

```language
// Advanced usage example
```

### Error Handling
Common errors and how to handle them.

### Notes
Additional considerations, performance notes, etc.
```

## API Documentation

### REST API Documentation Template

```markdown
## API Endpoint: [METHOD] /api/endpoint

### Description
What this endpoint does and its business purpose.

### HTTP Method
`POST`, `GET`, `PUT`, `DELETE`, etc.

### URL
```
https://api.example.com/v1/endpoint
```

### Authentication
- Required: Yes/No
- Type: Bearer Token, API Key, Basic Auth, etc.
- Headers: List required headers

### Request Parameters

#### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id        | string | Yes    | Resource identifier |

#### Query Parameters
| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| limit     | integer | No    | Number of results | 10 |
| offset    | integer | No    | Pagination offset | 0 |

#### Request Body
```json
{
  "field1": "string",
  "field2": 123,
  "field3": {
    "nested": "object"
  }
}
```

### Response Format

#### Success Response (200 OK)
```json
{
  "status": "success",
  "data": {
    // Response data structure
  },
  "meta": {
    "total": 100,
    "page": 1
  }
}
```

#### Error Responses
| Status Code | Description | Response Body |
|-------------|-------------|---------------|
| 400 | Bad Request | `{"error": "Invalid parameters"}` |
| 401 | Unauthorized | `{"error": "Authentication required"}` |
| 404 | Not Found | `{"error": "Resource not found"}` |
| 500 | Server Error | `{"error": "Internal server error"}` |

### Examples

#### cURL Example
```bash
curl -X POST https://api.example.com/v1/endpoint \
  -H "Authorization: Bearer your-token" \
  -H "Content-Type: application/json" \
  -d '{
    "field1": "value1",
    "field2": 123
  }'
```

#### JavaScript Example
```javascript
const response = await fetch('https://api.example.com/v1/endpoint', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer your-token',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    field1: 'value1',
    field2: 123
  })
});

const data = await response.json();
console.log(data);
```

#### Python Example
```python
import requests

response = requests.post(
    'https://api.example.com/v1/endpoint',
    headers={
        'Authorization': 'Bearer your-token',
        'Content-Type': 'application/json'
    },
    json={
        'field1': 'value1',
        'field2': 123
    }
)

data = response.json()
print(data)
```

### Rate Limiting
- Limit: 1000 requests per hour
- Headers: `X-RateLimit-Remaining`, `X-RateLimit-Reset`

### Versioning
- Current version: v1
- Deprecated versions: None
- Breaking changes: Will be announced 30 days in advance
```

## Function Documentation

### JavaScript/TypeScript Function Documentation

```javascript
/**
 * Calculates the total price including tax for a list of items.
 * 
 * @param {Array<Object>} items - Array of item objects
 * @param {number} items[].price - Price of individual item
 * @param {number} items[].quantity - Quantity of the item
 * @param {number} [taxRate=0.08] - Tax rate as decimal (default 8%)
 * @param {Object} [options={}] - Additional options
 * @param {boolean} [options.roundToCents=true] - Round result to nearest cent
 * @returns {number} Total price including tax
 * @throws {Error} When items array is empty or contains invalid data
 * 
 * @example
 * // Calculate total for shopping cart
 * const items = [
 *   { price: 10.99, quantity: 2 },
 *   { price: 5.50, quantity: 1 }
 * ];
 * const total = calculateTotalWithTax(items, 0.08);
 * console.log(total); // 29.73
 * 
 * @example
 * // With custom options
 * const total = calculateTotalWithTax(items, 0.08, { roundToCents: false });
 * console.log(total); // 29.7276
 */
function calculateTotalWithTax(items, taxRate = 0.08, options = {}) {
  if (!Array.isArray(items) || items.length === 0) {
    throw new Error('Items array cannot be empty');
  }
  
  const { roundToCents = true } = options;
  
  const subtotal = items.reduce((sum, item) => {
    if (typeof item.price !== 'number' || typeof item.quantity !== 'number') {
      throw new Error('Invalid item data: price and quantity must be numbers');
    }
    return sum + (item.price * item.quantity);
  }, 0);
  
  const total = subtotal * (1 + taxRate);
  
  return roundToCents ? Math.round(total * 100) / 100 : total;
}
```

### Python Function Documentation

```python
def calculate_total_with_tax(items: List[Dict[str, Union[float, int]]], 
                           tax_rate: float = 0.08,
                           round_to_cents: bool = True) -> float:
    """
    Calculate the total price including tax for a list of items.
    
    This function takes a list of items with price and quantity,
    applies the specified tax rate, and returns the total cost.
    
    Args:
        items (List[Dict[str, Union[float, int]]]): List of item dictionaries.
            Each item must have 'price' and 'quantity' keys.
        tax_rate (float, optional): Tax rate as decimal. Defaults to 0.08 (8%).
        round_to_cents (bool, optional): Whether to round to nearest cent. 
            Defaults to True.
    
    Returns:
        float: Total price including tax.
    
    Raises:
        ValueError: If items list is empty or contains invalid data.
        TypeError: If items is not a list or contains non-dict items.
    
    Examples:
        >>> items = [
        ...     {'price': 10.99, 'quantity': 2},
        ...     {'price': 5.50, 'quantity': 1}
        ... ]
        >>> calculate_total_with_tax(items)
        29.73
        
        >>> calculate_total_with_tax(items, tax_rate=0.10)
        32.03
        
        >>> calculate_total_with_tax(items, round_to_cents=False)
        29.7276
    
    Note:
        Tax calculation is applied to the entire subtotal, not per item.
        This follows standard retail tax calculation practices.
    """
    if not isinstance(items, list) or len(items) == 0:
        raise ValueError("Items must be a non-empty list")
    
    subtotal = 0.0
    for item in items:
        if not isinstance(item, dict):
            raise TypeError("Each item must be a dictionary")
        
        if 'price' not in item or 'quantity' not in item:
            raise ValueError("Each item must have 'price' and 'quantity' keys")
        
        try:
            price = float(item['price'])
            quantity = float(item['quantity'])
        except (ValueError, TypeError):
            raise ValueError("Price and quantity must be numeric")
        
        subtotal += price * quantity
    
    total = subtotal * (1 + tax_rate)
    
    return round(total, 2) if round_to_cents else total
```

## Component Documentation

### React Component Documentation

```jsx
import React, { useState, useCallback } from 'react';
import PropTypes from 'prop-types';

/**
 * ProductCard - A reusable card component for displaying product information
 * 
 * Features:
 * - Responsive design that adapts to container width
 * - Optional action buttons (Add to Cart, View Details)
 * - Lazy loading for product images
 * - Accessibility support with proper ARIA labels
 * - Customizable styling through CSS classes
 * 
 * @component
 * @example
 * // Basic usage
 * <ProductCard
 *   product={{
 *     id: 1,
 *     name: "Wireless Headphones",
 *     price: 99.99,
 *     image: "/images/headphones.jpg",
 *     description: "High-quality wireless headphones"
 *   }}
 *   onAddToCart={(product) => console.log('Added:', product)}
 * />
 * 
 * @example
 * // With custom styling and disabled state
 * <ProductCard
 *   product={product}
 *   className="custom-card"
 *   showActions={false}
 *   disabled={true}
 * />
 */
const ProductCard = ({
  product,
  onAddToCart,
  onViewDetails,
  showActions = true,
  className = '',
  disabled = false,
  ...props
}) => {
  const [imageLoaded, setImageLoaded] = useState(false);
  const [imageError, setImageError] = useState(false);

  const handleAddToCart = useCallback(() => {
    if (!disabled && onAddToCart) {
      onAddToCart(product);
    }
  }, [disabled, onAddToCart, product]);

  const handleViewDetails = useCallback(() => {
    if (!disabled && onViewDetails) {
      onViewDetails(product);
    }
  }, [disabled, onViewDetails, product]);

  return (
    <div 
      className={`product-card ${className} ${disabled ? 'disabled' : ''}`}
      data-testid="product-card"
      {...props}
    >
      <div className="product-image-container">
        {!imageError ? (
          <img
            src={product.image}
            alt={product.name}
            className={`product-image ${imageLoaded ? 'loaded' : 'loading'}`}
            onLoad={() => setImageLoaded(true)}
            onError={() => setImageError(true)}
            loading="lazy"
          />
        ) : (
          <div className="image-placeholder" aria-label="Image unavailable">
            📷
          </div>
        )}
      </div>
      
      <div className="product-info">
        <h3 className="product-name">{product.name}</h3>
        <p className="product-description">{product.description}</p>
        <div className="product-price">
          ${product.price.toFixed(2)}
        </div>
      </div>
      
      {showActions && (
        <div className="product-actions">
          <button
            onClick={handleAddToCart}
            disabled={disabled}
            className="btn btn-primary"
            aria-label={`Add ${product.name} to cart`}
          >
            Add to Cart
          </button>
          {onViewDetails && (
            <button
              onClick={handleViewDetails}
              disabled={disabled}
              className="btn btn-secondary"
              aria-label={`View details for ${product.name}`}
            >
              View Details
            </button>
          )}
        </div>
      )}
    </div>
  );
};

ProductCard.propTypes = {
  /** Product object containing all product information */
  product: PropTypes.shape({
    /** Unique product identifier */
    id: PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired,
    /** Product display name */
    name: PropTypes.string.isRequired,
    /** Product price in dollars */
    price: PropTypes.number.isRequired,
    /** Product image URL */
    image: PropTypes.string.isRequired,
    /** Product description text */
    description: PropTypes.string
  }).isRequired,
  
  /** Callback function called when Add to Cart is clicked */
  onAddToCart: PropTypes.func,
  
  /** Callback function called when View Details is clicked */
  onViewDetails: PropTypes.func,
  
  /** Whether to show action buttons */
  showActions: PropTypes.bool,
  
  /** Additional CSS class name */
  className: PropTypes.string,
  
  /** Whether the component is disabled */
  disabled: PropTypes.bool
};

export default ProductCard;
```

### CSS Documentation for Components

```css
/**
 * ProductCard Component Styles
 * 
 * Provides responsive card layout for product display with the following features:
 * - Mobile-first responsive design
 * - Hover effects and transitions
 * - Loading states for images
 * - Disabled state styling
 * - CSS Grid layout for consistent alignment
 * 
 * Usage:
 * Apply the .product-card class to the root element.
 * Customize appearance using CSS custom properties.
 * 
 * CSS Custom Properties:
 * --card-border-radius: Border radius for the card (default: 8px)
 * --card-shadow: Box shadow for the card (default: 0 2px 8px rgba(0,0,0,0.1))
 * --card-bg: Background color (default: #ffffff)
 * --primary-color: Primary button color (default: #007bff)
 * --text-color: Text color (default: #333333)
 */

.product-card {
  /* Layout */
  display: grid;
  grid-template-rows: auto 1fr auto;
  
  /* Appearance */
  background: var(--card-bg, #ffffff);
  border: 1px solid #e0e0e0;
  border-radius: var(--card-border-radius, 8px);
  box-shadow: var(--card-shadow, 0 2px 8px rgba(0, 0, 0, 0.1));
  
  /* Spacing */
  padding: 1rem;
  margin-bottom: 1rem;
  
  /* Transitions */
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  
  /* Interaction */
  cursor: pointer;
}

.product-card:hover:not(.disabled) {
  transform: translateY(-2px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
}

.product-card.disabled {
  opacity: 0.6;
  cursor: not-allowed;
  pointer-events: none;
}

/* Image Container */
.product-image-container {
  position: relative;
  width: 100%;
  height: 200px;
  overflow: hidden;
  border-radius: 4px;
  background: #f5f5f5;
  margin-bottom: 1rem;
}

.product-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: opacity 0.3s ease;
}

.product-image.loading {
  opacity: 0;
}

.product-image.loaded {
  opacity: 1;
}

.image-placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  font-size: 2rem;
  color: #999;
  background: #f0f0f0;
}

/* Product Information */
.product-info {
  margin-bottom: 1rem;
}

.product-name {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-color, #333);
  margin: 0 0 0.5rem 0;
  line-height: 1.3;
}

.product-description {
  color: #666;
  font-size: 0.9rem;
  line-height: 1.4;
  margin: 0 0 0.75rem 0;
  
  /* Limit to 2 lines */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.product-price {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-color, #007bff);
}

/* Action Buttons */
.product-actions {
  display: flex;
  gap: 0.5rem;
  margin-top: auto;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
  flex: 1;
}

.btn:hover:not(:disabled) {
  transform: translateY(-1px);
}

.btn:active:not(:disabled) {
  transform: translateY(0);
}

.btn:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}

.btn-primary {
  background: var(--primary-color, #007bff);
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover:not(:disabled) {
  background: #545b62;
}

/* Responsive Design */
@media (max-width: 768px) {
  .product-card {
    padding: 0.75rem;
  }
  
  .product-image-container {
    height: 150px;
  }
  
  .product-name {
    font-size: 1.1rem;
  }
  
  .product-price {
    font-size: 1.25rem;
  }
  
  .product-actions {
    flex-direction: column;
  }
}

@media (min-width: 1200px) {
  .product-image-container {
    height: 250px;
  }
}

/* Print Styles */
@media print {
  .product-card {
    box-shadow: none;
    border: 1px solid #ccc;
    break-inside: avoid;
  }
  
  .product-actions {
    display: none;
  }
}
```

## Language-Specific Guidelines

### JavaScript/TypeScript

#### JSDoc Standards
```javascript
/**
 * @fileoverview Utility functions for data processing
 * @author Your Name <your.email@example.com>
 * @version 1.2.0
 * @since 1.0.0
 */

/**
 * @typedef {Object} User
 * @property {string} id - Unique user identifier
 * @property {string} name - User's full name
 * @property {string} email - User's email address
 * @property {Date} createdAt - Account creation date
 */

/**
 * @namespace DataUtils
 * @description Collection of utility functions for data manipulation
 */
const DataUtils = {
  /**
   * Filters and sorts user data based on criteria
   * @memberof DataUtils
   * @param {User[]} users - Array of user objects
   * @param {Object} criteria - Filter criteria
   * @param {string} [criteria.nameFilter] - Filter by name substring
   * @param {Date} [criteria.createdAfter] - Filter by creation date
   * @param {string} [sortBy='name'] - Sort field
   * @returns {Promise<User[]>} Filtered and sorted users
   * @throws {TypeError} When users is not an array
   * @async
   * @example
   * const users = await DataUtils.filterUsers(allUsers, {
   *   nameFilter: 'john',
   *   createdAfter: new Date('2023-01-01')
   * });
   */
  async filterUsers(users, criteria, sortBy = 'name') {
    // Implementation
  }
};
```

### Python

#### Docstring Standards (Google Style)
```python
"""
Data processing utilities module.

This module provides utility functions for processing and manipulating
user data, including filtering, sorting, and validation operations.

Example:
    Basic usage of the module:

    >>> from data_utils import filter_users
    >>> users = [{"id": 1, "name": "John", "email": "john@example.com"}]
    >>> filtered = filter_users(users, name_filter="john")
    >>> print(len(filtered))
    1

Attributes:
    DEFAULT_SORT_FIELD (str): Default field for sorting operations.
    MAX_BATCH_SIZE (int): Maximum number of items to process in one batch.
"""

from typing import List, Dict, Optional, Union
from datetime import datetime

DEFAULT_SORT_FIELD = "name"
MAX_BATCH_SIZE = 1000


class UserDataProcessor:
    """A processor for user data operations.
    
    This class provides methods for filtering, sorting, and validating
    user data with built-in error handling and performance optimizations.
    
    Attributes:
        batch_size (int): Number of items to process per batch.
        strict_mode (bool): Whether to raise exceptions for data errors.
        
    Example:
        >>> processor = UserDataProcessor(batch_size=500)
        >>> filtered_users = processor.filter_users(users, {"active": True})
    """
    
    def __init__(self, batch_size: int = MAX_BATCH_SIZE, strict_mode: bool = True):
        """Initialize the UserDataProcessor.
        
        Args:
            batch_size: Number of items to process per batch. Must be positive.
            strict_mode: If True, raise exceptions for data errors. If False,
                log warnings and continue processing.
                
        Raises:
            ValueError: If batch_size is not positive.
        """
        if batch_size <= 0:
            raise ValueError("batch_size must be positive")
            
        self.batch_size = batch_size
        self.strict_mode = strict_mode
    
    def filter_users(self, 
                    users: List[Dict[str, Union[str, int, datetime]]], 
                    criteria: Dict[str, Union[str, datetime, bool]],
                    sort_by: str = DEFAULT_SORT_FIELD) -> List[Dict[str, Union[str, int, datetime]]]:
        """Filter and sort user data based on specified criteria.
        
        This method applies multiple filters to user data and returns
        the results sorted by the specified field. Processing is done
        in batches for memory efficiency with large datasets.
        
        Args:
            users: List of user dictionaries. Each user must have 'id',
                'name', and 'email' fields.
            criteria: Dictionary of filter criteria. Supported keys:
                - name_filter (str): Substring to match in user names
                - email_domain (str): Email domain to filter by
                - created_after (datetime): Minimum creation date
                - active (bool): Whether user is active
            sort_by: Field name to sort by. Must be a valid user field.
                
        Returns:
            List of user dictionaries matching the criteria, sorted by
            the specified field. Returns empty list if no matches found.
            
        Raises:
            TypeError: If users is not a list or contains non-dict items.
            ValueError: If sort_by field doesn't exist in user data.
            KeyError: If required user fields are missing (strict mode only).
            
        Example:
            >>> users = [
            ...     {"id": 1, "name": "John Doe", "email": "john@example.com", 
            ...      "created_at": datetime(2023, 1, 15), "active": True},
            ...     {"id": 2, "name": "Jane Smith", "email": "jane@company.com",
            ...      "created_at": datetime(2023, 2, 10), "active": False}
            ... ]
            >>> criteria = {
            ...     "name_filter": "john",
            ...     "created_after": datetime(2023, 1, 1),
            ...     "active": True
            ... }
            >>> processor = UserDataProcessor()
            >>> result = processor.filter_users(users, criteria)
            >>> print(len(result))
            1
            >>> print(result[0]["name"])
            John Doe
            
        Note:
            - Case-insensitive matching is used for string filters
            - Date filtering includes the boundary date
            - Large datasets are processed in batches for memory efficiency
            - Invalid data is handled according to strict_mode setting
        """
        # Implementation here
        pass
```

### Java

#### Javadoc Standards
```java
/**
 * Utility class for processing user data with filtering and sorting capabilities.
 * 
 * <p>This class provides static methods for common data processing operations
 * including filtering users by various criteria, sorting, and validation.
 * All methods are thread-safe and optimized for performance with large datasets.
 * 
 * <p><strong>Usage Example:</strong>
 * <pre>{@code
 * List<User> users = Arrays.asList(
 *     new User("1", "John Doe", "john@example.com"),
 *     new User("2", "Jane Smith", "jane@company.com")
 * );
 * 
 * FilterCriteria criteria = new FilterCriteria.Builder()
 *     .nameFilter("john")
 *     .activeOnly(true)
 *     .build();
 *     
 * List<User> filtered = UserDataProcessor.filterUsers(users, criteria);
 * }</pre>
 * 
 * @author Your Name
 * @version 2.1.0
 * @since 1.0.0
 * @see User
 * @see FilterCriteria
 */
public final class UserDataProcessor {
    
    /**
     * Default maximum number of users to process in a single batch.
     * <p>This value balances memory usage with processing efficiency.
     */
    public static final int DEFAULT_BATCH_SIZE = 1000;
    
    /**
     * Default field name for sorting operations when none is specified.
     */
    public static final String DEFAULT_SORT_FIELD = "name";
    
    // Private constructor to prevent instantiation
    private UserDataProcessor() {
        throw new UnsupportedOperationException("Utility class cannot be instantiated");
    }
    
    /**
     * Filters a list of users based on the specified criteria and returns them sorted.
     * 
     * <p>This method applies all non-null criteria from the {@link FilterCriteria} object
     * to filter the input list. The filtering operations include:
     * <ul>
     *   <li>Case-insensitive name substring matching</li>
     *   <li>Email domain filtering</li>
     *   <li>Date range filtering for account creation</li>
     *   <li>Active status filtering</li>
     * </ul>
     * 
     * <p>The method processes data in batches for memory efficiency when dealing
     * with large datasets (> {@value #DEFAULT_BATCH_SIZE} items).
     * 
     * @param users the list of users to filter; must not be {@code null} but may be empty
     * @param criteria the filtering criteria to apply; must not be {@code null}
     * @param sortBy the field name to sort by; must be a valid {@link User} field name
     * @return a new list containing users matching the criteria, sorted by the specified field;
     *         never {@code null} but may be empty if no users match
     * @throws IllegalArgumentException if any parameter is {@code null}, or if {@code sortBy}
     *                                  is not a valid field name
     * @throws IllegalStateException if the sorting operation fails due to data inconsistencies
     * 
     * @see #filterUsers(List, FilterCriteria)
     * @see FilterCriteria
     * @see User#getValidFieldNames()
     * 
     * @since 1.0.0
     */
    public static List<User> filterUsers(
            @NonNull List<User> users, 
            @NonNull FilterCriteria criteria, 
            @NonNull String sortBy) {
        
        // Parameter validation
        Objects.requireNonNull(users, "Users list cannot be null");
        Objects.requireNonNull(criteria, "Filter criteria cannot be null");
        Objects.requireNonNull(sortBy, "Sort field cannot be null");
        
        if (!User.getValidFieldNames().contains(sortBy)) {
            throw new IllegalArgumentException("Invalid sort field: " + sortBy);
        }
        
        // Implementation here...
        return new ArrayList<>();
    }
    
    /**
     * Filters users using default sorting by name.
     * 
     * <p>This is a convenience method equivalent to calling 
     * {@link #filterUsers(List, FilterCriteria, String)} with 
     * {@value #DEFAULT_SORT_FIELD} as the sort field.
     * 
     * @param users the list of users to filter
     * @param criteria the filtering criteria to apply
     * @return filtered and sorted list of users
     * @throws IllegalArgumentException if any parameter is {@code null}
     * 
     * @see #filterUsers(List, FilterCriteria, String)
     * @since 1.0.0
     */
    public static List<User> filterUsers(@NonNull List<User> users, @NonNull FilterCriteria criteria) {
        return filterUsers(users, criteria, DEFAULT_SORT_FIELD);
    }
}

/**
 * Represents filtering criteria for user data operations.
 * 
 * <p>This class uses the builder pattern to construct filtering criteria
 * in a fluent and readable manner. All criteria are optional and are
 * combined using logical AND operations.
 * 
 * <p><strong>Example:</strong>
 * <pre>{@code
 * FilterCriteria criteria = new FilterCriteria.Builder()
 *     .nameFilter("john")
 *     .emailDomain("example.com")
 *     .createdAfter(LocalDate.of(2023, 1, 1))
 *     .activeOnly(true)
 *     .build();
 * }</pre>
 * 
 * @since 1.0.0
 */
public static final class FilterCriteria {
    
    private final Optional<String> nameFilter;
    private final Optional<String> emailDomain;
    private final Optional<LocalDate> createdAfter;
    private final Optional<Boolean> activeOnly;
    
    /**
     * Builder class for constructing {@link FilterCriteria} instances.
     * 
     * <p>This builder provides a fluent interface for setting filtering
     * criteria. All methods return the builder instance for method chaining.
     * 
     * @since 1.0.0
     */
    public static final class Builder {
        // Builder implementation...
    }
}
```

## Documentation Tools and Automation

### Automated Documentation Generation

#### For JavaScript/TypeScript Projects
```json
{
  "devDependencies": {
    "@microsoft/api-extractor": "^7.36.0",
    "@microsoft/api-documenter": "^7.22.0",
    "typedoc": "^0.24.0",
    "jsdoc": "^4.0.0"
  },
  "scripts": {
    "docs:generate": "typedoc src --out docs --theme default",
    "docs:api": "api-extractor run && api-documenter markdown -i temp -o docs/api",
    "docs:serve": "npx http-server docs -p 8080"
  }
}
```

#### TypeDoc Configuration (typedoc.json)
```json
{
  "entryPoints": ["src/index.ts"],
  "out": "docs",
  "theme": "default",
  "includeVersion": true,
  "excludePrivate": true,
  "excludeProtected": true,
  "excludeExternals": true,
  "readme": "README.md",
  "name": "Project API Documentation",
  "navigationLinks": {
    "GitHub": "https://github.com/user/repo"
  }
}
```

#### For Python Projects
```python
# requirements-dev.txt
sphinx>=5.0.0
sphinx-autodoc-typehints>=1.19.0
sphinx-rtd-theme>=1.2.0
myst-parser>=0.18.0

# conf.py for Sphinx
extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.viewcode',
    'sphinx.ext.napoleon',
    'sphinx_autodoc_typehints',
    'myst_parser'
]

autodoc_default_options = {
    'members': True,
    'member-order': 'bysource',
    'special-members': '__init__',
    'undoc-members': True,
    'exclude-members': '__weakref__'
}

napoleon_google_docstring = True
napoleon_numpy_docstring = False
```

### Documentation Linting and Quality Checks

#### ESLint JSDoc Plugin Configuration
```json
{
  "plugins": ["jsdoc"],
  "rules": {
    "jsdoc/check-alignment": "error",
    "jsdoc/check-examples": "error",
    "jsdoc/check-indentation": "error",
    "jsdoc/check-param-names": "error",
    "jsdoc/check-syntax": "error",
    "jsdoc/check-tag-names": "error",
    "jsdoc/check-types": "error",
    "jsdoc/implements-on-classes": "error",
    "jsdoc/match-description": "error",
    "jsdoc/newline-after-description": "error",
    "jsdoc/no-undefined-types": "error",
    "jsdoc/require-description": "error",
    "jsdoc/require-description-complete-sentence": "error",
    "jsdoc/require-example": "error",
    "jsdoc/require-hyphen-before-param-description": "error",
    "jsdoc/require-param": "error",
    "jsdoc/require-param-description": "error",
    "jsdoc/require-param-name": "error",
    "jsdoc/require-param-type": "error",
    "jsdoc/require-returns": "error",
    "jsdoc/require-returns-check": "error",
    "jsdoc/require-returns-description": "error",
    "jsdoc/require-returns-type": "error",
    "jsdoc/valid-types": "error"
  }
}
```

## Testing Documentation Examples

### Automated Testing of Documentation Examples

#### JavaScript/TypeScript Example Testing
```javascript
// test/docs-examples.test.js
/**
 * Tests that verify all code examples in documentation work correctly.
 * This ensures documentation stays in sync with actual implementation.
 */

import { describe, it, expect } from 'vitest';
import { calculateTotalWithTax } from '../src/utils/pricing';

describe('Documentation Examples', () => {
  describe('calculateTotalWithTax function examples', () => {
    it('should match basic usage example from docs', () => {
      // Example from documentation
      const items = [
        { price: 10.99, quantity: 2 },
        { price: 5.50, quantity: 1 }
      ];
      const total = calculateTotalWithTax(items, 0.08);
      
      // Should match documented result
      expect(total).toBe(29.73);
    });
    
    it('should match custom options example from docs', () => {
      const items = [
        { price: 10.99, quantity: 2 },
        { price: 5.50, quantity: 1 }
      ];
      const total = calculateTotalWithTax(items, 0.08, { roundToCents: false });
      
      // Should match documented result
      expect(total).toBeCloseTo(29.7276, 4);
    });
  });
});
```

#### Python Doctest Integration
```python
def calculate_total_with_tax(items, tax_rate=0.08, round_to_cents=True):
    """
    Calculate total with tax.
    
    >>> items = [{'price': 10.99, 'quantity': 2}, {'price': 5.50, 'quantity': 1}]
    >>> calculate_total_with_tax(items)
    29.73
    >>> calculate_total_with_tax(items, tax_rate=0.10)
    32.03
    """
    # Implementation here
    pass

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

## Maintenance and Updates

### Documentation Review Checklist

- [ ] **Accuracy**: All examples run without errors
- [ ] **Completeness**: All public APIs are documented
- [ ] **Clarity**: Examples are easy to understand
- [ ] **Consistency**: Follows established formatting standards
- [ ] **Currency**: Documentation reflects latest code changes
- [ ] **Accessibility**: Documentation is accessible to new developers
- [ ] **Searchability**: Key terms and concepts are properly tagged

### Automation Setup

#### GitHub Actions for Documentation
```yaml
name: Documentation

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  docs-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run docs:generate
      - run: npm run test:docs-examples
      
  docs-deploy:
    needs: docs-test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run docs:generate
      - uses: actions/deploy-pages@v4
        with:
          artifact_name: docs
          path: docs/
```

## Next Steps

1. **Set up documentation tooling** based on your chosen technology stack
2. **Create documentation templates** for your specific use cases
3. **Implement automated testing** for documentation examples
4. **Establish review processes** for keeping documentation current
5. **Set up automation** for generating and deploying documentation

This framework provides a solid foundation for comprehensive API documentation. Adapt the examples and templates to match your specific project requirements and technology stack.