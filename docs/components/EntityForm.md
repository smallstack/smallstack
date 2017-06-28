# Entity Form Component

The Entity Form Component can display a form with all properties of a type. 


## Example
```html
<EntityForm [model]="navigationEntry" (onSubmit)="saveNavigationEntryChanges($event)">
    <div class="row">
        <div class="col-lg-2 col-md-4 col-sm-6 col-12">
            <EntityFormField name="label"></EntityFormField>
        </div>
        <div class="col-lg-2 col-md-4 col-sm-6 col-12">
            <EntityFormField name="icon"></EntityFormField>
        </div>
        <div class="col-lg-2 col-md-4 col-sm-6 col-12">
            <EntityFormField name="defaultRoute"></EntityFormField>
        </div>
    </div>
</EntityForm>
```

This documentation is incomplete.
