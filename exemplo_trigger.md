delimiter $$
create function rt_percentual_comissao(vn_n_numevende int)
	return float
	deterministic
	begin
	declare percentual_comissao float(10,2);

	select n_porcvende into percentual_comissao from comvende
	where n_numevende = vn_n_numevende;

	return percentual_comissao;

	$$
	delimiter ;
##Exemplo de trigger before

delimiter $$
create trigger tri_vendas_bi
before insert on comvenda
for each row
begin
declare percentual_comissao float(10,2);
declare valor_comissao float(10,2);
## busco o percentual de comissão que o vendedor deve
## receber
select rt_percentual_comissao(new.n_numevende)
into percentual_comissao;
## calculo a comissão
set valor_comissao = ((total_venda * comissao) / 100);
## recebo no novo valor de comissão
set new.n_vcomvenda = valor_comissao;
end
$$
delimiter ;


delimiter $$
create trigger tri_vendas_bu
	before update on comvenda
	for each row

	begin
	declare percentual_comissao float(10,2);
	declare total_venda float(10,2);
	declare valor_comissao float(10,2);

	if(old.n_totavenda <> new.n_totavenda) then
	select rt_percentual_comissao(new.n_numevende)
	into percentual_comissao;

	valor_comissao = ((total_venda * comissao)/100);

	set new.n_vcomvenda = valor_comissao;
	end if;
	end
	$$
	delimiter ; 

##Exemplo de trigger after

delimiter $$
create trigger tri_vendas_ai
	after insert on comivenda
	for each row
	begin
	#declaro as variáveis que utilizarei
	declare vtotal_itens float(10,2);
	declare vtotal_item float(10,2);
	declare total_item float(10,2);

	##cursor para buscar os itens já registrados da venda
	declare busca_itens cursor for
	select  n_totaivenda
	from comivenda
	where n_numevenda = new.n_numevenda;

	open busca_itens;
	itens : loop

	fetch busca_itens into total_item;
	set vtotal_itens = vtotal_itens + total_item;

	end loop itens;

	close busca_itens;

	update comvenda set n_totavenda = vtotal_itens 
		where n_numevenda = new.n_numevenda;

		end
		$$
		delimiter ;
