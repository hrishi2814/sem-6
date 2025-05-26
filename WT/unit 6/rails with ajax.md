# Rails with AJAX (5 Marks)

## 1. Basic Concept of AJAX in Rails (1 Mark)

AJAX (Asynchronous JavaScript and XML) in Rails allows:
- Partial page updates without full reloads
- Asynchronous server communication
- Enhanced user experience through responsive interfaces

Rails provides built-in support via:
- `remote: true` option in helpers
- JS templates (`.js.erb`)
- UJS (Unobtrusive JavaScript) driver

## 2. Implementing AJAX (2 Marks)

### Controller Setup:
```ruby
def update
  @item = Item.find(params[:id])
  respond_to do |format|
    if @item.update(item_params)
      format.html { redirect_to @item }
      format.js   # Looks for update.js.erb
    else
      format.html { render :edit }
      format.js { render :update_error }
    end
  end
end
```

### View with remote: true:
```erb
<%= form_with(model: @item, remote: true) do |form| %>
  <!-- form fields -->
<% end %>

<%= link_to "Delete", item_path(@item), 
    method: :delete, 
    remote: true,
    data: { confirm: "Are you sure?" } %>
```

### JavaScript Response (update.js.erb):
```erb
// Update DOM element
document.getElementById("item-<%= @item.id %>").innerHTML = 
  "<%= j render @item %>";

// Show flash message
document.getElementById("flash").innerHTML = 
  "<div class='alert alert-success'>Updated successfully!</div>";
```

## 3. Handling Responses (1 Mark)

Rails can respond with:
- HTML (full page)
- JavaScript (`.js.erb` templates)
- JSON (for API responses)

```ruby
respond_to do |format|
  format.html
  format.js
  format.json { render json: @item }
end
```

## 4. Error Handling (0.5 Mark)

```erb
// update_error.js.erb
document.getElementById("errors").innerHTML = 
  "<%= j render 'shared/errors', object: @item %>";
```

## 5. Advantages (0.5 Mark)

- Faster page interactions
- Reduced server load
- Better user experience
- Seamless integration with Rails conventions

Key Points for Exam:
1. Always mention `remote: true`
2. Show understanding of `respond_to` block
3. Demonstrate JS template usage
4. Include error handling
5. Highlight performance benefits

---
