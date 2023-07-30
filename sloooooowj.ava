package misc;

import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;

public class main_misc {

	public static List<String> word_list = new ArrayList<>();
	public static HashMap<Integer,List<String>> word_cache = new HashMap<>();
	
	public static int MAX = 100;
	
	public static void main(String[] args) {
	
		try {
			BufferedReader rd = new BufferedReader(new FileReader("src\\abandon.txt"));
			String line;
			while((line = rd.readLine()) != null){
				word_list.add(line);
			}
			
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		int max_len = set_cache();
		
		/*List<String> test = new ArrayList<>(Arrays.asList("horn","pato","mato"));
		System.out.println(get_prefix(test,1,4));*/
		
		/*List<String> test = new ArrayList<>();
		System.out.println(make_rectangle(4,4,new ArrayList<>(),0,test));
		System.out.println(test);*/
		
		get_max_rectangle(max_len);
		
	}
	
	//1) divide the words in groups based on the lengths of the strings
	private static int set_cache(){
		
		int max = 0;
		
		for(int i = 0;i < word_list.size();i++){
			String word = word_list.get(i);
			int len = word.length();
			if(len > max) {
				max = len;
			}
			
			if(!word_cache.containsKey(len)){
				word_cache.put(len,new ArrayList<>(Arrays.asList(word)));
			}
			else {
				word_cache.get(len).add(word);
			}
		}
		
		return max;
	}
	
	/*Instead of forcing the rectangle to appear its better to just test the cases and see if its correct,i can use
	 * some rules to terminate a process that i now that will result in a wrong rectangle 
	 */
	
	private static List<String> get_prefix(List<String> rectangle,int idx,int a){
		
		/*	horn
		 * 	pato
		 * 	mato
		 * 
		 * idx 1 prefix = {hp,oa,rt,no}
		 */
		
		List<String> prefix = new ArrayList<>();
		
		for(int i = 0;i < a;i++){
			
			StringBuilder str = new StringBuilder();
			for(int j = 0;j <= idx;j++){
				str.append(rectangle.get(j).substring(i,i+1));
			}
			prefix.add(str.toString());
			
		}
		
		
		return prefix;
	}
	
	private static boolean check_prefix(List<String> prefix,int b){
		
		Tree_char cache_b = new Tree_char(word_cache.get(b));
		
		for(int i = 0;i < prefix.size();i++){
			
			if(!cache_b.have_word(prefix.get(i))){//this method checks prefixes too
				return false;
			}
			
		}
		return true;
		
	}
	
	private static boolean end_branch(List<String> rectangle,int idx,int a,int b){
		
		List<String> prefix = get_prefix(rectangle,idx,a);
		
		return !check_prefix(prefix,b);
		
	}
	
	private static boolean make_rectangle(int a,int b,List<String> rectangle,int last_idx,List<String> cpy){
		
		if(last_idx-1 == b){
			return true;
		}
		
		//if i put a word in the list and there is a prefix that does not exist on the cache then i terminate the branch
		if(last_idx > 0 && end_branch(rectangle,last_idx-1,a,b)){
			//rectangle = new ArrayList<>();
			return false;
		}
		
		List<String> cache_a = word_cache.get(a);
		
		if(cache_a == null) {
			return false;
		}
		
		for(int i = 0;i < cache_a.size();i++){
			
			List<String> tmp = new ArrayList<>();
			tmp.addAll(rectangle);
			tmp.add(cache_a.get(i));
			if(make_rectangle(a,b,tmp,last_idx+1,cpy)){
				if(tmp.size()-1 == b){
					tmp.remove(tmp.size()-1);
					cpy.addAll(tmp);
				}
				rectangle.addAll(tmp);
				
				//System.out.println(tmp);
				return true;
			}
		}
		
		return false;
	}
	
	private static List<String> get_max_rectangle(int max_len){
		
		List<String> max_list = new ArrayList<>();
		int max = 0;
		int c = 0;
		for(int i = 1;i <= max_len;i++){
			
			for(int j = 1;j <= max_len;j++){
				
				List<String> list = new ArrayList<>();
				if(make_rectangle(i,j,new ArrayList<>(),0,list)){
					int l = list.size();
					if(l > max){
						max  = l;
						max_list = list;
						System.out.println("-> "+l);
						for(int k = 0;k < max_list.size();k++){
							System.out.println(max_list.get(k));
						}
						System.out.println("------------");
						break;
					}
				}
				c++;
			}
			if(c >= MAX){
				break;
			}
		}
		
		
		
		for(int i = 0;i < max_list.size();i++){
			System.out.println(max_list.get(i));
		}
		
		return max_list;
	}
	
}
