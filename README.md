# LEARN Notes Application

### Getting Started

1. You must have the following dependencies installed:

   - Ruby 3
     - See [`.ruby-version`](.ruby-version) for the specific version.
   - Node 19
     - See [`.nvmrc`](.nvmrc) for the specific version.
   - PostgreSQL 14
   - Redis 6.2
   - [Chrome](https://www.google.com/search?q=chrome) (for headless browser tests)

2. Run the `bin/setup` script.
3. Start the application with `bin/dev`.
4. Visit http://localhost:3000.

## Information about Bullet Train

If this is your first time working on a Bullet Train application, be sure to review the [Bullet Train Basic Techniques](https://bullettrain.co/docs/getting-started) and the [Bullet Train Developer Documentation](https://bullettrain.co/docs).

### Render

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/bullet-train-co/bullet_train)

Clicking this button will take you to the first step of a process that, when completed, will provision production-grade infrastructure for your Bullet Train application which will cost about **$30/month**.

When you're done deploying to Render, you need to go into "Dashboard" > "web", copy the server URL, and then go into "Env Groups" > "settings" and paste the URL into the value for `BASE_URL`.

https://github.com/bullet-train-co/bullet_train.git

git@github.com:bullet-train-co/bullet_train.git

git clone git@github.com:bullet-train-co/bullet_train.git your_new_project_name

bin/super-scaffold crud Note Team title:text_field body:text_area

1. If you would like the table view you've just generated to reactively update when a Note is updated on the server, please edit `app/models/team.rb`, locate the `has_many :notes`, and add `enable_cable_ready_updates: true` to it.

app/model/note.rb (done)
class Note < ApplicationRecord

# 🚅 add concerns above.

# 🚅 add attribute accessors above.

belongs_to :team
belongs_to :creator, class_name: "Membership"

# 🚅 add belongs_to associations above.

# 🚅 add has_many associations above.

has_rich_text :body

# 🚅 add has_one associations above.

# 🚅 add scopes above.

validates :creator, scope: true

# 🚅 add validations above.

# 🚅 add callbacks above.

# 🚅 add delegations above.

def valid_creators
team.users
end

# 🚅 add methods above.

end

app/views/account/notes/\_form.html.erb
on line 9 (done)
<%= render 'shared/fields/super_select', method: :creator_id, options: {autofocus: true}, html_options: {autofocus: true},
choices: @note.valid_creators.map { |membership| [membership.label_string, membership.id] } %>

app/views/account/notes/\_index.html.erb
line 26

<th><%= t('.fields.creator.heading') %></th>

app/views/account/notes/\_note.html.erb
line 10 (done)

<td><%= render 'shared/attributes/belongs_to', attribute: :creator, url: [:account, note] %></td>

app/views/account/notes/show.html.erb
Line 14 (done)
<%= render 'shared/attributes/belongs_to', attribute: :creator %>
