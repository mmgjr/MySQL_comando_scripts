set global event_scheduler = on;

create event processa_comissao on schedule every 1 week starts '2019-01-05 23:30:00'
	do
		begin
		call processa_comissionamento(
			current_date()-interval 7 day,current_date(),@a);
		end
		$$
		delimiter ;
