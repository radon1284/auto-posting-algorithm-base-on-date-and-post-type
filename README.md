# Auto posting algorithm base on date and post type

```ruby
namespace :auto_status do
  desc "Add Status to the Tracking code Automaticaly"
  task make_status: :environment do
  	@product_trackers = ProductTracker.all
  	@statuses = Status.all
  	@date = DateTime.now.utc
	# Status.where(product_tracker_id: product_tracker.id).count == 1
	@product_trackers.each do |product_tracker|

			if (Status.where(product_tracker_id: product_tracker.id).count == 1 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 1)

				@links = Status.new
				@links.order_status = 1
				@links.product_tracker_id = product_tracker.id

				@links.save
			elsif (Status.where(product_tracker_id: product_tracker.id).count == 2 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 2)

				@links = Status.new
				@links.order_status = 2
				@links.product_tracker_id = product_tracker.id

				@links.save
			elsif (Status.where(product_tracker_id: product_tracker.id).count == 3 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 5)

				@links = Status.new
				@links.order_status = 3
				@links.product_tracker_id = product_tracker.id

				@links.save
			elsif (Status.where(product_tracker_id: product_tracker.id).count == 4 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 6)
				
				@links = Status.new
				@links.order_status = 4
				@links.product_tracker_id = product_tracker.id

				@links.save
			end
	end

  end

end
```
