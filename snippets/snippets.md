# Odoo Snippets

## Create a new model

```python
from dateutil import relativedelta
from odoo import _, models, fields, api
from odoo.exceptions import ValidationError, UserError

class MyModel(models.Model):
    _name = 'my.model'
    _description = 'My Model'

    name = fields.Char(
        string='Name',
        required=True
    )
    description = fields.Text(
        string='Description'
    )
```

## All metadata

### Normal Model

```python
    _name = 'model.name'
    _description = 'Description'
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]
```

### Copy Inherited Model

```python
    _name = 'model2.name'
    _description = 'Description'
    _inherit = 'model.name'
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]
```

### Extend Inherited Model

```python
    _inherit = 'model.name'
    _description = 'Description'
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]
```

## All fields types

```python
    # Basic fields
    char = fields.Char(
        string='label',
        required=False,
        default='Default',
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    text = fields.Text(
        string='label',
        required=False,
        default='Default',
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    integer = fields.Integer(
        string='label',
        required=False,
        default=0,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    float_val = fields.Float(
        string='label',
        required=False,
        default=0.0,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    boolean = fields.Boolean(
        string='label',
        required=False,
        default=False,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    date = fields.Date(
        string='label',
        required=False,
        default=fields.Date.today,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    datetime = fields.Datetime(
        string='label',
        required=False,
        default=fields.Datetime.now,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    selection = fields.Selection(
        string='label',
        required=False,
        selection=[('value', 'Label')],
        default='value',
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    extended_selection = fields.Selection(
        string='label',
        required=False,
        selection_add=[('value', 'Label')],
        default='value',
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    binary = fields.Binary(
        string='label',
        required=False,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    html = fields.Html(
        string='label',
        required=False,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    related = fields.Related(
        string='label',
        related='field_name.subfield_name',
    )
    monetary = fields.Monetary(
        string='label',
        required=False,
        default=0.0,
        readonly=False,
        copy=True,
        help='Help message here.'
    )

    # Relational fields
    many2one = fields.Many2one(
        string='label',
        comodel_name='table.name',
        default=1,
        ondelete='restrict',
        domain=[('field', '=', 'value')],
        required=False,
        readonly=False,
        copy=True,
        help='Help message here.'
    )
    one2many = fields.One2many(
        string='label',
        comodel_name='table.name',
        inverse_name='field_name',
        readonly=False,
        help='Help message here.'
    )
    many2many = fields.Many2many(
        string='label',
        comodel_name='table.name',
        relation='table_name',
        column1='field_name',
        column2='field_name',
        readonly=False,
        help='Help message here.'
    )

    # Computed fields
    computed_field = fields.Char(
        string='label',
        compute='_compute_field',
        inverse='_inverse_field',
        store=False,
        help='Help message here.'
    )

    @api.depends('field_name')
    def _compute_computed_field(self):
        for record in self:
            record.computed_field = 'value'

    def _inverse_computed_field(self):
        for record in self:
            record.field_name = 'value'

    # Related fields
    related_field = fields.Char(
        string='label',
        related='field_name.subfield_name',
        store=False,
        depends=['dependent_field'],
        help='Help message here.'
    )

    # Custom display name
    def _compute_display_name(self):
        for record in self:
            record.display_name = 'value'

    # Default values
    field_name = fields.Char(
        string='label',
        default=lambda self: self._default_field_name(),
        help='Help message here.'
    )

    def _default_field_name(self):
        for record in self:
            record.field_name = 'value'

    # Hierarchical fields
    _parent_store = True
    _parent_name = 'parent_id'
    parent_id = fields.Many2one(
        string='label',
        comodel_name='table.name',
        ondelete='restrict',
        index=True,
        help='Help message here.'
    )
    parent_path = fields.Char(
        index=True,
    )
    child_ids = fields.One2many(
        string='label',
        comodel_name='table.name',
        inverse_name='parent_id',
        help='Help message here.'
    )

    @api.constrains('parent_id')
    def _check_hierarchy(self):
        if not self._check_recursion():
            raise ValidationError(_('Error! The record cannot create recursive hierarchy.'))
```

## Method Decorators

```python
    @api.model
    def method_name(self):
        for record in self:
            pass

    @api.onchange('field_name')
    def _onchange_field_name(self):
        for record in self:
            pass

    @api.constrains('field_name')
    def _check_field_name(self):
        for record in self:
            if condition:
                raise ValidationError(_('Error message'))

    @api.depends('dependency_field')
    def _compute_field_name(self):
        for record in self:
            pass

    @api.depends_context('key')
    def _compute_field_name(self):
        for record in self:
            pass

    @api.ondelete(at_uninstall=False)
    def _unlink_if_condition(self):
        for record in self:
            if condition:
                raise UserError(_('Error message'))
```

## CRUD Methods

```python

    rec = Model.create({
        'field_name': 'value'
    })

    def create(self, vals):
        record = super(MyModel, self).create(vals)
        return record

    rec.write({
        'field_name': 'value'
    })

    def write(self, vals):
        res = super(MyModel, self).write(vals)
        return res

    result = rec.unlink()

    def unlink(self):
        res = super(MyModel, self).unlink()
        return res

    result = rec.copy()

    def copy(self, default=None):
        record = super(MyModel, self).copy(default=default)
        return record

    result = rec.browse([1])

    result = rec.read(['field_name'])

    result = rec.search([('field_name', '=', 'value')])

    result = rec.search_count([('field_name', '=', 'value')])

    result = rec.read_group(
        domain=[('field_name', '=', 'value')],
        fields=['aggregated_field'],
        groupby=['group_by_field'],
        offset=0,
        limit=None,
        orderby=False,
        lazy=False
    )

    result = rec._read_group(
        domain=[('field_name', '=', 'value')],
        groupby=['group_by_field'],
        aggregates=['agg_field:agg_func'],
        having=[('field_name', '=', 'value')],
        offset=0,
        limit=None,
        order=None
    )
```

## Inheritance

- Copy Inheritance

```python
    _name = 'model2.name'
    _description = 'Description'
    _inherit = 'model.name'
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]
```

- Extend Inheritance

```python
    _inherit = 'model.name'
    _description = 'Description'
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]
```

````Delegation Inheritance

```python
    _name = 'model2.name'
    _description = 'Description'
    _inherits = {'model.name': 'field_name'}
    _order = 'field_name'
    _sql_constraints = [
        ('field_name_unique', 'UNIQUE(field_name)', 'Error message')
    ]

    field_name = fields.Many2one(
        comodel_name='model.name',
        string='label',
        required=True,
        ondelete='cascade'
    )
````

## Actions

### Server Action

```python
    def action_name(self):
        for record in self:
            pass
```

### Client Action

```python
    def action_name(self):
        return {
            'type': 'ir.actions.client',
            'tag': 'action_name',
            'name': 'Action Name',
            'context': {
                'key': 'value'
            }
        }
```
