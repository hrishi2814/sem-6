# **Handling Document Requests in Rails**

In Rails, handling document requests (such as PDFs, Excel files, or CSV exports) typically involves generating files on the server and sending them as downloadable responses. Below are different approaches to implement document requests:

---

## **1. Generating & Downloading PDFs (Using Prawn or Wicked PDF)**
### **Option A: Using Prawn (Pure Ruby PDF Generation)**
1. **Add Prawn to Gemfile:**
   ```ruby
   gem 'prawn'
   gem 'prawn-table' # Optional (for tables)
   ```

2. **Create a PDF Service:**
   ```ruby
   # app/services/pdf_generator.rb
   class PdfGenerator
     def self.generate(user)
       Prawn::Document.new do |pdf|
         pdf.text "User Report", size: 24, style: :bold
         pdf.move_down 20
         pdf.text "Name: #{user.name}"
         pdf.text "Email: #{user.email}"
       end
     end
   end
   ```

3. **Controller Action to Download PDF:**
   ```ruby
   # app/controllers/reports_controller.rb
   def download_pdf
     user = User.find(params[:id])
     pdf = PdfGenerator.generate(user)
     send_data pdf.render, 
       filename: "user_report.pdf",
       type: "application/pdf",
       disposition: "attachment"
   end
   ```

4. **Route:**
   ```ruby
   get '/users/:id/download_pdf', to: 'reports#download_pdf', as: 'download_pdf'
   ```

---

### **Option B: Using Wicked PDF (HTML-to-PDF Conversion)**
1. **Install Wicked PDF & wkhtmltopdf:**
   ```ruby
   gem 'wicked_pdf'
   gem 'wkhtmltopdf-binary' # For Heroku/Linux
   ```

2. **Controller Setup:**
   ```ruby
   def download_pdf
     @user = User.find(params[:id])
     respond_to do |format|
       format.pdf do
         render pdf: "user_report",
                template: "reports/show.html.erb",
                disposition: "attachment"
       end
     end
   end
   ```

3. **Create a PDF View (`app/views/reports/show.html.erb`):**
   ```html
   <h1>User Report</h1>
   <p>Name: <%= @user.name %></p>
   <p>Email: <%= @user.email %></p>
   ```

4. **Route:**
   ```ruby
   get '/users/:id/report.pdf', to: 'reports#download_pdf', as: 'user_report'
   ```

---

## **2. Generating & Downloading Excel/CSV Files**
### **Option A: Using CSV Library (Built-in Ruby)**
```ruby
def export_csv
  @users = User.all
  respond_to do |format|
    format.csv do
      headers['Content-Disposition'] = "attachment; filename=users.csv"
      headers['Content-Type'] ||= 'text/csv'
    end
  end
end
```

**View (`app/views/users/export.csv.erb`):**
```erb
<%= CSV.generate do |csv|
  csv << ["ID", "Name", "Email"]
  @users.each do |user|
    csv << [user.id, user.name, user.email]
  end
end.html_safe %>
```

### **Option B: Using Axlsx (For Excel Files)**
1. **Add Gem:**
   ```ruby
   gem 'axlsx'
   ```

2. **Controller Action:**
   ```ruby
   def export_excel
     @users = User.all
     respond_to do |format|
       format.xlsx do
         render xlsx: "users_report", filename: "users.xlsx"
       end
     end
   end
   ```

3. **View (`app/views/users/export_excel.xlsx.axlsx`):**
   ```ruby
   wb = xlsx_package.workbook
   wb.add_worksheet(name: "Users") do |sheet|
     sheet.add_row ["ID", "Name", "Email"]
     @users.each do |user|
       sheet.add_row [user.id, user.name, user.email]
     end
   end
   ```

---

## **3. Sending Files from Storage (Active Storage)**
If the file is already stored (e.g., in S3 or local storage):

```ruby
def download_file
  user = User.find(params[:id])
  if user.document.attached?
    redirect_to rails_blob_url(user.document, disposition: "attachment")
  else
    redirect_to root_path, alert: "File not found."
  end
end
```

---

## **4. Streaming Large Files (Avoiding Memory Issues)**
For large files, use **`send_file` with streaming**:
```ruby
def download_large_file
  file_path = Rails.root.join('private', 'large_report.pdf')
  send_file file_path, 
    filename: "large_report.pdf",
    type: "application/pdf",
    disposition: "attachment",
    stream: true,
    buffer_size: 4096
end
```

---

## **5. Key Methods for File Downloads**
| Method | Usage |
|--------|-------|
| `send_data` | Sends raw binary data (PDF, CSV, etc.) |
| `send_file` | Sends a file from disk/storage |
| `rails_blob_url` | Generates a download link for Active Storage files |
| `render pdf: ...` | (Wicked PDF) Renders HTML as PDF |

---

## **Conclusion**
- **PDFs**: Use **Prawn** (for code-based PDFs) or **Wicked PDF** (HTML-to-PDF).
- **Excel/CSV**: Use **CSV** (built-in) or **Axlsx** (for Excel).
- **Stored Files**: Use **Active Storage** with `rails_blob_url`.
- **Large Files**: Use `send_file` with `stream: true`.

This covers the most common ways to handle document requests in Rails efficiently. 🚀