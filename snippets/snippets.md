## Table of Contents

- [Model Initialization](#model-initialization)
  - [`odoo-model`](#odoo-model)
  - [`odoo-copy-model`](#odoo-copy-model)
  - [`odoo-extend-model`](#odoo-extend-model)
- [Field Definitions](#field-definitions)
  - [`odoo-char-field`](#odoo-char-field)
  - [`odoo-text-field`](#odoo-text-field)
  - [`odoo-integer-field`](#odoo-integer-field)
  - [`odoo-float-field`](#odoo-float-field)
  - [`odoo-boolean-field`](#odoo-boolean-field)
  - [`odoo-date-field`](#odoo-date-field)
  - [`odoo-datetime-field`](#odoo-datetime-field)
  - [`odoo-selection-field`](#odoo-selection-field)
  - [`odoo-xtended-selection-field`](#odoo-xtended-selection-field)
  - [`odoo-monetary-field`](#odoo-monetary-field)
  - [`odoo-binary-field`](#odoo-binary-field)
  - [`odoo-html-field`](#odoo-html-field)
  - [`odoo-related-field`](#odoo-related-field)
  - [`odoo-currency-id`](#odoo-currency-id)
  - [`odoo-many2one-field`](#odoo-many2one-field)
  - [`odoo-one2many-field`](#odoo-one2many-field)
  - [`odoo-many2many-field`](#odoo-many2many-field)
  - [`odoo-computed-field`](#odoo-computed-field)
- [API Methods](#api-methods)
  - [`odoo-api-model`](#odoo-api-model)
  - [`odoo-api-onchange`](#odoo-api-onchange)
  - [`odoo-api-constraint`](#odoo-api-constraint)
  - [`odoo-api-depends`](#odoo-api-depends)
  - [`odoo-api-depends-context`](#odoo-api-depends-context)
  - [`odoo-api-ondelete`](#odoo-api-ondelete)
- [Error Handling](#error-handling)
  - [`odoo-raise-user-error`](#odoo-raise-user-error)
  - [`odoo-raise-validation-error`](#odoo-raise-validation-error)
- [Record Operations](#record-operations)
  - [`odoo-create-record`](#odoo-create-record)
  - [`odoo-override-create-record`](#odoo-override-create-record)
  - [`odoo-write-record`](#odoo-write-record)
  - [`odoo-override-write-record`](#odoo-override-write-record)
  - [`odoo-copy-record`](#odoo-copy-record)
  - [`odoo-override-copy-record`](#odoo-override-copy-record)
  - [`odoo-unlink-record`](#odoo-unlink-record)
  - [`odoo-override-unlink-record`](#odoo-override-unlink-record)
  - [`odoo-browse-record`](#odoo-browse-record)
  - [`odoo-read-record`](#odoo-read-record)
  - [`odoo-search-record`](#odoo-search-record)
  - [`odoo-search-count-record`](#odoo-search-count-record)
  - [`odoo-read-group-record`](#odoo-read-group-record)
  - [`odoo-aggregate-read-group-record`](#odoo-aggregate-read-group-record)
- [Miscellaneous](#miscellaneous)
  - [`odoo-display-name`](#odoo-display-name)
  - [`odoo-default-function`](#odoo-default-function)
  - [`odoo-server-action`](#odoo-server-action)

### Model Initialization

#### `odoo-model`

```python
from dateutil import relativedelta
from odoo import _, models, fields, api
from odoo.exceptions import ValidationError, UserError

class LibraryTestBook(models.Model):
    _name = 'library.test.book'
    _description = 'library.test.book'
    _order = 'id'
    _sql_constraints = [('chk_field_name', 'SQL_CONSTRAINT', 'Error Message')]

    name = fields.Char(
        string='Name',
        required=True
    )
    description = fields.Text(
        string='Description'
    )
```

#### `odoo-copy-model`

```python
from dateutil import relativedelta
from odoo import _, models, fields, api
from odoo.exceptions import ValidationError, UserError

class LibraryTestBook(models.Model):
    _name = 'library.test.book'
    _description = 'library.test.book'
    _inherit = 'inherit.model'
    _order = 'id'
    _sql_constraints = [('chk_field_name', 'SQL_CONSTRAINT', 'Error Message')]

    name = fields.Char(
        string='Name',
        required=True
    )
    description = fields.Text(
        string='Description'
    )
```

#### `odoo-extend-model`

```python
from dateutil import relativedelta
from odoo import _, models, fields, api
from odoo.exceptions import ValidationError, UserError

class LibraryTestBook(models.Model):
    _inherit = 'inherit.model'
```

### Field Definitions

#### `odoo-char-field`

```python
    field_name = fields.Char(
        string='Field Name',
        required=True,
        default='default_value',
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-text-field`

```python
    field_name = fields.Text(
        string='Field Name',
        required=True,
        default='default_value',
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-integer-field`

```python
    field_name = fields.Integer(
        string='Field Name',
        required=True,
        default=0,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-float-field`

```python
   field_name = fields.Float(
        string='Field Name',
        digits=(16,2),
        required=True,
        default=0.0,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-boolean-field`

```python
    field_name = fields.Boolean(
        string='Field Name',
        required=True,
        default=True,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-date-field`

```python
    field_name = fields.Date(
        string='Field Name',
        required=True,
        default=fields.Date.today,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-datetime-field`

```python
    field_name = fields.Datetime(
        string='Field Name',
        required=True,
        default=fields.Datetime.now,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-selection-field`

```python
    field_name = fields.Selection(
        string='Field Name',
        required=True,
        selection=[('value', 'Label')],
        default='value',
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-xtended-selection-field`

```python
    field_name = fields.Selection(
        string='Field Name',
        required=True,
        selection_add=[('value', 'Label')],
        default='value',
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-monetary-field`

```python
field_name = fields.Monetary(
        string='Field Name',
        required=True,
        default=0.0,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-binary-field`

```python
    field_name = fields.Binary(
        string='Field Name',
        required=True,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-html-field`

```python
    field_name = fields.Html(
        string='Field Name',
        required=True,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-related-field`

```python
    field_name = fields.Char(
        string='field_name',
        related='field_id.field_name',
        store=False,
        depends=['dependent_field'],
        help='Help message...'
    )
```

#### `odoo-currency-id`

```python
    currency_id = fields.Many2one(
        comodel_name='res.currency',
        default=lambda self: self.env.company.currency_id,
        required=True,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-many2one-field`

```python
    field_name = fields.Many2one(
        string='Field Name',
        comodel_name='table.name',
        default=default_value,
        ondelete='restrict',
        domain=[('field', '=', 'value')],
        required=True,
        readonly=True,
        copy=True,
        help='Help message...'
    )
```

#### `odoo-one2many-field`

```python
    field_name = fields.One2many(
        string='Field Name',
        comodel_name='table.name',
        inverse_name='field_name',
        readonly=True,
        help='Help message...'
    )
```

#### `odoo-many2many-field`

```python
    field_name = fields.Many2many(
        string='Field Name',
        comodel_name='table.name',
        relation='table_name',
        column1='field_name',
        column2='field_name',
        readonly=True,
        help='Help message...'
    )
```

#### `odoo-computed-field`

```python
    field_name = fields.Char(
        string='Field Name',
        compute='_compute_field_name',
        inverse='_inverse_field_name',
        store=False,
        help='Help message...'
    )

@api.depends('field_name')
def _compute_field_name(self):
    for record in self:
        record.field_name = value

def _inverse_field_name(self):
    for record in self:
        record.field_name = value
```

### API Methods

#### `odoo-api-model`

```python
@api.model
def method_name(self, arg):
    for record in self:
        pass
```

#### `odoo-api-onchange`

```python
@api.onchange('field_name')
def _onchange_field_name(self):
    for record in self:
        pass
```

#### `odoo-api-constraint`

```python
@api.constrains('field_name')
def _check_field_name(self):
    for record in self:
        pass
```

#### `odoo-api-depends`

```python
@api.depends('dependency_field')
def _compute_field_name(self):
    for record in self:
        pass
```

#### `odoo-api-depends-context`

```python
@api.depends_context('dependency_key')
def _compute_field_name(self):
    for record in self:
        pass
```

#### `odoo-api-ondelete`

```python
@api.ondelete(at_uninstall=False)
def _unlink_if_condition(self):
    for record in self:
        pass
```

### Error Handling

#### `odoo-raise-user-error`

```python
raise UserError(_('Error message...'))
```

#### `odoo-raise-validation-error`

```python
raise ValidationError(_('Error message...'))
```

### Record Operations

#### `odoo-create-record`

```python
record_name = self.env['model.name'].create({
    'field_name': 'value'
})
```

#### `odoo-override-create-record`

```python
def create(self, vals):
    record = super(LibraryTestBook, self).create(vals)
    return record
```

#### `odoo-write-record`

```python
record_name.write({
    'field_name': 'value'
})
```

#### `odoo-override-write-record`

```python
def write(self, vals):
    record = super(LibraryTestBook, self).write(vals)
    return record
```

#### `odoo-copy-record`

```python
record_name.copy({
    'field_name': 'value'
})
```

#### `odoo-override-copy-record`

```python
def copy(self, default=None):
    record = super(LibraryTestBook, self).copy(default)
    return record
```

#### `odoo-unlink-record`

```python
record_name.unlink()
```

#### `odoo-override-unlink-record`

```python
def unlink(self):
    record = super(LibraryTestBook, self).unlink()
    return record
```

#### `odoo-browse-record`

```python
result = self.env['model.name'].browse([record_id])
```

#### `odoo-read-record`

```python
result = self.env['model.name'].read([field_name])
```

#### `odoo-search-record`

```python
result = self.env['model.name'].search([('field_name', '=', 'value')])
```

#### `odoo-search-count-record`

```python
result = self.env['model.name'].search_count([('field_name', '=', 'value')])
```

#### `odoo-read-group-record`

```python
result = self.env['model.name'].read_group(
    domain=[('field_name', '=', 'value')],
    fields=['aggregated_field'],
    groupby=['group_by_field'],
    offset=0,
    limit=None,
    orderby=False,
    lazy=False
)
```

#### `odoo-aggregate-read-group-record`

```python
result = self.env['model.name']._read_group(
    domain=[('field_name', '=', 'value')],
    groupby=['group_by_field'],
    aggregates=['agg_field:agg_func'],
    having=[('field_name', '=', 'value')],
    offset=0,
    limit=None,
    order=None
)
```

### Miscellaneous

#### `odoo-display-name`

```python
def _compute_display_name(self):
    for record in self:
        record.display_name = new_value
```

#### `odoo-default-function`

```python
def _default_field_name(self):
    for record in self:
        record.field_name = default_value
```

#### `odoo-server-action`

```python
def method_name(self, arg):
    for record in self:
        pass
```
