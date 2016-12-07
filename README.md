# Auto posting algorithm base on date and post type

```ruby
namespace :auto_status do
  desc "Add Status to the Tracking code Automaticaly"
  task make_status: :environment do
    order_status = 0
    ProductTracker.find_in_batches(batch_size: 1000) do | group |
      group.each | product_tracker |
        # These queries on the if conditions can be optimized if you use counter_cache
      	if (Status.where(product_tracker_id: product_tracker.id).count == 1 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 1)
	  order_status = 1
	elsif (Status.where(product_tracker_id: product_tracker.id).count == 2 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 2)
	  order_status = 2
	elsif (Status.where(product_tracker_id: product_tracker.id).count == 3 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 5)
	  order_status = 3
	 elsif (Status.where(product_tracker_id: product_tracker.id).count == 4 && (((Time.parse(DateTime.now.to_s) - Time.parse(Status.where(product_tracker_id: product_tracker.id).first.created_at.to_s))/1.days).round) == 6)
	   order_status = 4
	 end
	 product_tracker.status.create(order_status: order_status)
      end
    end
  end

end
```
