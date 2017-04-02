# woo-commerce-categories
In this session we display all the categories with it's Product Counting e.g. Clothing(20).
<?PHP
  $args = array(
	'number'     => $number,
	'orderby'    => 'name',
	'order'      => 'ASC',
	'hide_empty' => $hide_empty,
	'include'    => $ids
	);

$product_categories = get_terms( 'product_cat', $args );
<div  class="container">
	<div class="col-md-2 text-left bg-danger">
  /* In this section Display categories with it's subcategories and product counting  */
		<div class="row">
			<ul class="list-group list-unstyled">
			<?php foreach ($product_categories as $key => $categories)
			{
				if($categories->parent==0)
				{
					?>
					<li class="sidebar-brand">
	                    <!-- <span class="glyphicon glyphicon-plus"></span> -->
	                    <a href="<?php echo get_term_link( $categories->term_id, 'product_cat' ); ?>">
	                        <?php echo $categories->name." (".$categories->count.")"; ?>
	                    </a>
	                    <?php
	                    $term_children = get_term_children( $categories->term_id, 'product_cat' );
	                   	if($term_children>0)
	                   	{
	                   		echo "<ul class='list-unstyled category_ul_style'>";
	                   		foreach ($term_children as $key => $subcategories)
	                   		{
	                   			$term = get_term( $subcategories, 'product_cat' );
	                   			?>
	                   			<li class="list-unstyled"><span class="glyphicon glyphicon-plus"></span><span><a href="<?php echo get_term_link( $subcategories, 'product_cat' ) ?>"><?php echo $term->name."(".$term->count.")"; ?></a></span></li>
	                   			
	                   			<?php
	                   		}
	                   		echo "</ul>";
	                   	}
	                    ?>
	                </li>
	                <?php
				}
			} 
			?>
			</ul>
		</div>
	</div>
<div class="col-md-9">
/* Put another Content  */
</div>
?>
