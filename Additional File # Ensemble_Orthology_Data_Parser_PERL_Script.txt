#!/usr/bin/perl -w
#Generate a hash of orthology groups with associated gene names
use strict;
use warnings;

my $orthogroupfile = $ARGV[0];

open (ORTHOGROUPFH, $orthogroupfile) or die "Can't open < $orthogroupfile";

my @grouparray = <ORTHOGROUPFH>;

my $countoutputfile = "Orthology_Group_Count_Data.out";
my $groupoutputfile = "Orthology_Group_Summary.out";
my $idsoutputfile = "Orthology_Group_Gene_IDs_and_Group_Numbers.out";

open (my $countoutputfh, ">" , $countoutputfile) or die "Can't open $countoutputfile";
open (my $idsoutputfh, ">", $idsoutputfile) or die "Can't open $idsoutputfile";
open (my $groupoutputfh, ">", $groupoutputfile) or die "Can't open $groupoutputfile";

my $groupnumber = 0;
my $genecount;
my @groupcountarray;
my @groupgeneidarray;
my @speciesarray;
my @genearray;

foreach my $groups (@grouparray){
	undef @groupcountarray;
	undef @groupgeneidarray;
	push @groupcountarray, $groupnumber;
	push @groupgeneidarray, $groupnumber;
	chomp $groups;
#	print $groupoutputfh "$groups\n";
	@speciesarray = split /\t/, $groups, -1;
#	print $groupoutputfh join("\t",@speciesarray),"\n";
	foreach my $species (@speciesarray){
		@genearray = split /,/, $species;
		$genecount = scalar @genearray;
		push @groupcountarray, $genecount;
		foreach my $geneid (@genearray){
			push @groupgeneidarray, $geneid;
			print "$geneid\t$groupnumber\n";
			print $idsoutputfh "$geneid\t$groupnumber\n";
		}
	}
	print join("\t",@groupcountarray),"\n";
	print join("\t",@groupgeneidarray),"\n";
	print $groupoutputfh join("\t",@groupcountarray),"\t";
	print $groupoutputfh join("\t",@groupgeneidarray),"\n";
	$groupnumber++;
}

close ORTHOGROUPFH;
exit