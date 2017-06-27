# List Component
The List Component is a very generic component, basically to show a list of items. The items can either be set via the attribute `models`, via socket or directly via a service query.

## Examples

### Basic Usage with local models
```html
<List [models]="players"></List>
```
This will render a rather unattractive list of all items!


### Service Query with inner template
```html
<List serviceQuery="playerService.getAllPlayers" serviceQueryPageSize="15">
  <ng-template #entryTemplate let-player="model">
    <div class="card">
      <div class="card-header">{{player.name}}</div>
      <div class="card-block">Points: {{player.points}}</div>
    </div>
  </ng-template>
</List>
```
