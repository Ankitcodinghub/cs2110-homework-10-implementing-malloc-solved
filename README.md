# cs2110-homework-10-implementing-malloc-solved
**TO GET THIS SOLUTION VISIT:** [CS2110 Homework 10-Implementing Malloc Solved](https://www.ankitcodinghub.com/product/cs2110-homework-10-implementing-malloc-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;92786&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS2110 Homework 10-Implementing Malloc Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
<div class="page" title="Page 1">
<div class="layoutArea">
<div class="column"></div>
</div>
</div>
<div class="page" title="Page 2">
<div class="layoutArea">
<div class="column">
Purpose

The purpose of this assignment is to give you a deeper understanding of some of the most important functions in C: malloc, free, calloc, and realloc. These four functions are key to writing programs that can handle dynamic amounts of data, like strings of arbitrary lengths and practically unlimited amounts of user input. Knowing how to use these functions is vital, but it is also important to understand how they work–especially if you are a Devices, Info Internetworks, or Systems/Architecture student who will be taking CS 2200 (and possibly also CS 3210) in a later semester.

1.2 Tasks

You will be implementing the backend of the four core functions for dynamic allocation: malloc, free, calloc, and realloc. While calloc and realloc can be implemented in terms of malloc and free, malloc and free must be implemented from scratch, using a freelist of pointers to keep track of available memory and the sbrk function to obtain more memory when needed.

There are also several helper functions included that you may want to implement. These functions are not graded, but we may provide test cases that help ensure your implementations of these functions are sound. You are not required to use and/or complete any of the helper functions, although you may find the homework a lot easier to complete if you do.

1.3 Criteria

You will be graded using an autograder with several test cases, similar to Homework 9. Each of the four functions will be tested with cases that test different behaviors; for example, one case might expect malloc to find and return a perfectly sized free block, while other cases expect malloc to split a larger block into two.

2 Assignment

In this assignment, you will be writing the dynamic memory allocation and deallocation functions of malloc, free, realloc, and calloc. These functions are confusing to write, so we have provided an in-depth guide below. Please read through this entire pdf before beginning. The specifics for each function are located in malloc.c as well as in the subsections below.

2.1 The Basics

It is the job of the memory allocator to process and satisfy the memory requests of the user. But where does the allocator get its memory? Let us recall the structure of a program’s memory footprint.

</div>
</div>
<div class="layoutArea">
<div class="column">
2

</div>
</div>
</div>
<div class="page" title="Page 3">
<div class="layoutArea">
<div class="column">
+——————-+ (low memory) | CODE | +——————-+

| DATA | +——————-+ &lt;– Break || || +——————-+

<pre>                           |       STACK       |
                           +-------------------+ (high memory)
</pre>
When a program is loaded into memory there are various “segments” created for different purposes: code, stack, data, etc. In order to create some dynamic memory space, otherwise known as the heap, it is possible to move the “break”, which is the first address after the end of the process’s uninitialized data segment. A function called brk() is provided to set this address to a different value. There is also a function called sbrk() which moves the break by some amount specified as a parameter.

<pre>                           +-------------------+ (low memory)
                           |       CODE        |
                           +-------------------+
                           |       DATA        |
                           +-------------------+
</pre>
| HEAP | +——————-+ &lt;– New Break || || +——————-+

| STACK | +——————-+ (high memory)

For simplicity, a wrapper for the system call sbrk() has been provided for you as a function called my sbrk located in suites/malloc suite.c. Make sure to use this call rather than a real call to sbrk, as doing this can potentially cause a lot of problems during program execution. Note that any problems introduced by calling the real sbrk will not be regraded, so make sure that everything is correct before turning in.

If you glance at the code for my sbrk(), you will quickly notice that upon the first call it always allocates 8 KiB. For the purposes of your program, you should treat the returned amount as whatever you requested. For instance, the first time I call my sbrk() it will be done like this:

<pre>                      my_sbrk(SBRK_SIZE); /* SBRK_SIZE == 2 KB */
</pre>
—————————————–

| 8KB | —————————————–

^

|

\______ The pointer returned to me by my_sbrk

Even though you have a full 8 KiB, you should treat it as if you were only returned SBRK SIZE bytes. Now when you run out of memory and need more heap space you will need to call my sbrk() again. Once again, the call is simply:

</div>
</div>
<div class="layoutArea">
<div class="column">
3

</div>
</div>
</div>
<div class="page" title="Page 4">
<div class="layoutArea">
<div class="column">
<pre>my_sbrk(SBRK_SIZE);
</pre>
</div>
</div>
<div class="layoutArea">
<div class="column">
—————————————– |2KB| 6KB | —————————————–

<pre>                             ^
                             |
                             \____ The pointer returned to me by my_sbrk
</pre>
Notice how it returned a pointer to the address after the end of the 2 KB I had requested the first time. my sbrk() remembers the end of the data segment you request each time and is able to return that value to you as the beginning of the new data segment on a following call. Keep this in mind as you write the assignment!

We’ve written my sbrk to be able to only hand out a certain amount of memory before returning -1 to indicate that its done. This limit gives us the ability to test the behavior of the code when my sbrk can’t get more memory.

2.2 Block Allocation

Trying to use sbrk() (or brk()) exclusively to provide dynamic memory allocation to your program would be very difficult and inefficient. Calling sbrk() involves a decent amount of system overhead, and we would prefer not to have to call it every single time a small amount of memory is required. In addition, deallocation would be a problem. Say we allocated several 100 byte chunks of memory and then decided we were done with the first. Where would the break be? There’s no handy function to move the break back, so how could we reuse that first 100 byte chunk?

What we need are a set of functions that manage a pool of memory allowing us to allocate and deallocate efficiently. Typically, such schemes start out with no free memory at all. The first time the user requests memory, the allocator will call sbrk() as discussed above to obtain a relatively large chunk of memory. The user will be given a block with as much free space as they requested, and if there is any memory left over it will be managed by placing information about that left over block of memory in a data structure where information about all such free blocks is kept. This is called the freelist and we will return to this later.

In order to keep track of allocated blocks we will create a structure to store the information we need to know about a block. Where should we store this structure? We can’t simply call malloc() to allocate space, since we’re writing the function, and that’d lead to infinite recursion! However, there’s an easier way that will keep our bookkeeping structure right with the data we’re allocating for easy access.

In order to keep track of allocated blocks, we will create a structure to store the information we need to know about a block, also known as metadata, inside the block itself. The metadata contains two things: a pointer to the next node in the freelist, and the size of the user data section. Both of these are required in order to accurately keep track of the memory available in the freelist.

Figure 1. The metadata is placed before the user data. The next byte after the end of the metadata is the first byte that can be given to the user.

We will need to take into consideration the leading metadata whenever we allocate blocks. To let the user have as much space as they requested, when they request a block of size n bytes we will allocate a block of size sizeof(the metadata) + n. The size requested by the user will be stored in the metadata; additionally, the metadata will contain a pointer to the next metadata struct in the freelist. As depicted in my malloc.h, this is the struct definition for the metadata:

</div>
</div>
<table>
<tbody>
<tr>
<td>
<div class="layoutArea">
<div class="column">
Metadata

</div>
</div>
</td>
<td>
<div class="layoutArea">
<div class="column">
User Data

</div>
</div>
</td>
</tr>
</tbody>
</table>
<div class="layoutArea">
<div class="column">
4

</div>
</div>
</div>
<div class="page" title="Page 5">
<div class="layoutArea">
<div class="column">
<pre>                             typedef struct metadata {
                                 struct metadata *next_size;
                                 unsigned long size;
</pre>
<pre>                             } metadata_t;
</pre>
The size portion of the metadata struct contains the size that the user requested. In order to get the total size of the block, we add this size with sizeof(metadata_t), which is the size in bytes of the metadata. For ease of reading, this size will be represented as TMS (total metadata size) in all of our block representation diagrams. The user does not care about the metadata for the block, they just want the size they requested. Therefore, when you return a block to the user, you will need to use pointer arithmetic to ’step over’ the metadata and return the address of the data. What this looks like:

Pointer returned to the user

Figure 2. When a block is returned to the user, the pointer returned points to the beginning address of the area used by the user.

2.3 The Freelist

When we split up memory, we give one piece/block to the user. The remaining pieces/blocks are placed in a linked list, called the freelist, to be used at a later time. For this semester, we are representing our freelist as a single singly linked list that is organized by the address in ascending order. This linked list will be defined as a global file variable and to help you out, we have already defined it for you.

</div>
</div>
<table>
<tbody>
<tr>
<td>
<div class="layoutArea">
<div class="column">
Metadata

</div>
</div>
</td>
<td>
<div class="layoutArea">
<div class="column">
User Data

</div>
</div>
</td>
</tr>
</tbody>
</table>
<div class="layoutArea">
<div class="column">
<pre>                                  metadata_t *addr_list;
</pre>
To help visualize this, below we have an example representation of our freelist.

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A Meta Size: TMS

addr list Usable Size: 3 Total:3+TMS

</div>
<div class="column">
block in use by the user

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 30

Total:30+TMS

</div>
<div class="column">
block in use by the user

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 10

Total:10+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
Note: The name of the blocks refer to their address order. For example, since the letter B comes after the letter A, Block B starts at an address after Block A.

For the remainder of the pdf, we will represent the freelist without spaces for the blocks currently in use by the user like so:

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A Meta Size: TMS

<ol>
<li>First Line: The name of the block (“Block B”) – Note that the name refers to the ordering that the blocks should be in.</li>
<li>Second Line: Meta Size → The size of the metadata for that block</li>
<li>Third Line: Usable Size → The size of the space available to the user</li>
<li>Fourth Line: Total → The total size of the memory taken up by this block</li>
</ol>
</div>
</div>
<div class="layoutArea">
<div class="column">
Block B Meta Size: TMS Usable Size: 30

Total:30+TMS

A Quick Note: The node representations in our freelists should be read as the following:

</div>
</div>
<div class="layoutArea">
<div class="column">
addr list Usable Size: 3 Total:3+TMS

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 10

</div>
</div>
<div class="layoutArea">
<div class="column">
5

</div>
</div>
<div class="layoutArea">
<div class="column">
Total:10+TMS

</div>
</div>
</div>
<div class="page" title="Page 6">
<div class="layoutArea">
<div class="column">
Since the addr list is singly linked, be sure to properly update the next pointer when adding and removing nodes from the list.

2.4 Simple Linked List: Allocating

When we first allocate space for the heap, it is in our best interest not to just request what we need immediately but rather to get a sizable amount of space, use a piece of it now, and keep the rest around in the freelist until we need it. This reduces the amount of times we need to call sbrk(), the real version of which, as we discussed earlier, involves significant system overhead. So how do we know how much to allocate, how much to give to the user, and how much to keep?

For this assignment we will request blocks of size 2048 bytes from my sbrk(). We don’t want to waste space, though, so we want to give to the user the smallest size block in which their request would fit. For example, the user may request 256 bytes of space. It is tempting to give them a block that is 256 bytes, but remember we are also storing the metadata inside the block. If our metadata takes up sizeof (metadata t) = 16 bytes for example, we need at least a

256+16 = 272

byte block.

Note that the size of your metadata will vary based on your computer’s architecture and platform. Use sizeof() to avoid depending on the platform, specifically sizeof(metadata_t) when doing math with the metadata size.

How do we get from one big free block of size 2048 bytes to the block of size 272 bytes we want to give to the user? In this simple implementation, you will traverse the addr list to find the best block to satisfy the user’s request, which should be equal or greater than the size requested, and “split” off however much you need from the front or the back. For this assignment, you must split off from the back.

</div>
</div>
<div class="layoutArea">
<div class="column">
Say we have the following situation:

Block A Meta Size: TMS

addr list Usable Size: 50 Total:50+TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 15

Total:15+TMS

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 100

Total:100+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
When we malloc for a certain size, we first want to use a block of that exact or best size, remove it from both the addr list and return it to the user.

</div>
</div>
<div class="layoutArea">
<div class="column">
Ex: malloc(15) would leave the freelist as so:

Block A Meta Size: TMS

room to hold the user’s requested data. There are actually two cases to consider:

<ul>
<li>If a block’s user data size is at least requested_size + MS + 1, then you should split the block into two halves. The right split should become its own block, with its own metadata and requested_size bytes in the user data section. This is the block that will eventually be returned to the user. We need to update the left split to reflect its new user data size of old_size – MS – requested_size. Note that the user size is still at least 1 byte, making it a valid block. This block should remain in the freelist.</li>
<li>If a block’s user data size is smaller than requested_size + MS + 1, then splitting the block would 6</li>
</ul>
</div>
</div>
<div class="layoutArea">
<div class="column">
Block C Meta Size: TMS Usable Size: 100

Total:100+TMS

If we do not have a perfectly sized block, then we will return the smallest block in the list that has enough

</div>
</div>
<div class="layoutArea">
<div class="column">
addr list Usable Size: 50 Total:50+TMS

</div>
</div>
</div>
<div class="page" title="Page 7">
<div class="layoutArea">
<div class="column">
not leave enough room for the metadata and at least a byte of user data. So, instead of splitting, return the whole block, even though the user gets a bit more space then they need.

In the following diagram, the requested size is 25 bytes, and the first block has enough room:

</div>
</div>
<div class="layoutArea">
<div class="column">
addr list Usable Size: 25 – TMS Total:25

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A’ Meta Size: TMS

</div>
<div class="column">
Block A Meta Size: TMS Usable Size: 25

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 15

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 100

Total:100+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
Total: 25+TMS

Once Block A is returned to the user, this call will leave the freelist as such:

</div>
</div>
<div class="layoutArea">
<div class="column">
Total:15+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
addr list Usable Size: 25 – TMS Total: 25

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A’ Meta Size: TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 35

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 100

</div>
</div>
<div class="layoutArea">
<div class="column">
Total: 35 + TMS

Don’t forget to move the pointer to the beginning of the space the user uses at the end of the metadata

before returning the block to the user.

2.5 Simple Linked List: Deallocating

When we deallocate memory, we simply return the block to the addr list in the appropriate position. When the user calls the free function with a block body pointer, we do some pointer arithmetic to find the starting point of the entire block (i.e. the start of the metadata). Notice we don’t clear out all the data. That simply takes too long when we’re not supposed to care about what’s in memory after we free it anyway. For all of you who were wondering why sometimes you can still access data in a dynamically allocated block even after you call free on its pointer, this is why!

We like the freelists to contain fairly large blocks so that large requests can be allocated quickly, so if the block on either side of the block we’re freeing is also free, we can coalesce them, or join them into the bigger block like they were before we split them.

How do we know which blocks we can join together? If adding a free block’s address and the block’s total size (both TMS and the user data size) gives you the address of another free block’s metadata, then you know that those two blocks are next to each other in memory, so they can be merged. If A has a size of M and B has a size of N, then if they are next to each other in memory, you can merge them to create a new block of size M+N+TMS.

Whenever you deallocate a block, you must merge it with nearby free blocks if possible. There are a couple of ways to do this:

<ul>
<li>A simple technique is to search the freelist for blocks that are next to the newly freed block. Concep- tually, it looks like this:
<ul>
<li>– &nbsp;Given a block B, iterate through the free list and find a block A that is located directly to the left of B in memory. This means that if we take the A’s address and add A’s total size, we line up perfectly with B’s address, meaning there are no gaps between A and B. If this block exists, we can merge A/B, then remove A from the freelist.</li>
<li>– &nbsp;We can do the same procedure for blocks that are located directly to the right of B in memory. Again, if a block C exists, we merge B/C and remove C from the freelist.</li>
<li>– &nbsp;Finally, we re-insert B or our newly merged blocks back into the freelist. Don’t forget to keep nodes sorted by address!</li>
</ul>
</li>
<li>We can optimize this process by simply adding the newly freed block to the freelist first, then scanning through the list for blocks to merge. Since the freelist is sorted by address, two blocks MUST be next to each other in the freelist in order to be next to each other in memory. This means you can go through every pair of consecutive elements in the freelist, check if the blocks are touching in memory,</li>
</ul>
</div>
</div>
<div class="layoutArea">
<div class="column">
7

</div>
</div>
<div class="layoutArea">
<div class="column">
Total: 100 + TMS

</div>
</div>
</div>
<div class="page" title="Page 8">
<div class="layoutArea">
<div class="column">
and merge them if necessary. When merging contiguous blocks, it is recommended to leave the left block in the freelist and grow its size, while removing the right block.

</div>
</div>
<div class="layoutArea">
<div class="column">
Here’s an example of how to free and merge blocks:

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A Meta Size: TMS

addr list Usable Size: 8 Total:8+TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 3

Total:3+TMS

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 10

Total:10+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
If we deallocated a block of size 6 (Block D), we would first iterate through the addr list for the correct left and right addresses of the block and check to see if the block needs to be merged either to the right of left. In this example, the block to be entered is not directly next to any other blocks in memory, so we would just insert it into the addr list. This would leave the freelist as seen below.

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A Meta Size: TMS

addr list Usable Size: 8 Total:8+TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 3

Total:3+TMS

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 10

Total:10+TMS

</div>
<div class="column">
Block D Meta Size: TMS Usable Size: 6

Total:6+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
If Block C and D were right next to each other in memory (i.e. the address at end of block C is equal to the address at the beginning of block D), then we would need to perform a left merge. To perform this left merge, pop block C from the addr list , add block D to it, reset the size, and add it to the addr list in the same position that block C was in. Note that this series of steps assumes that you have not yet added D to the freelist. These steps are depicted below.

Remove Block C from the free list and merge it with Block D to make Block C’.

</div>
</div>
<div class="layoutArea">
<div class="column">
Block C Meta Size: TMS Usable Size: 10

Total:10+TMS

</div>
<div class="column">
Block D Meta Size: TMS Usable Size: 6

Total:6+TMS

</div>
<div class="column">
Block C’

Meta Size: TMS Usable Size: 16+TMS

Total:16+2·TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
Add this new block C’ back into the freelist in its proper position.

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A Meta Size: TMS

addr list Usable Size: 8 Total:8+TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 3

Total:3+TMS

</div>
<div class="column">
Block C’

Meta Size: TMS Usable Size: 16+TMS

Total:16+2·TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
If instead of a Block D we had a Block A∗ which was located right before Block A in memory (i.e. the address at the end of block A∗ is equal to the address at the beginning of block A), then we would need to perform a right merge. To perform this right merge, pop block A from the addr_list, add block A∗ to it, move block A’s metadata to block A∗, reset the size, and put the block back where block A originally was in the addr list.

Remove Block A from the free list and merge it with Block A∗ to form Block A’.

</div>
</div>
<div class="layoutArea">
<div class="column">
8

</div>
</div>
</div>
<div class="page" title="Page 9">
<div class="layoutArea">
<div class="column">
Block A∗ Meta Size: TMS Usable Size: 6

Total:6+TMS

</div>
<div class="column">
Block A Meta Size: TMS Usable Size: 8

Total:8+TMS

</div>
<div class="column">
Block A’

Meta Size: TMS Usable Size: 14+TMS

Total:14+2·TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
Add this new block A’ back into the freelist in its proper position.

</div>
</div>
<div class="layoutArea">
<div class="column">
Block A’ Meta Size: TMS

addr list Usable Size: 14+TMS Total:14+2·TMS

</div>
<div class="column">
Block B Meta Size: TMS Usable Size: 3

Total:3+TMS

</div>
<div class="column">
Block C Meta Size: TMS Usable Size: 10

Total:10+TMS

</div>
</div>
<div class="layoutArea">
<div class="column">
Note: To compare pointers (addresses), cast them to uintptr t first

2.6 my malloc()

</div>
</div>
<div class="layoutArea">
<div class="column">
You are to write your own version of malloc that implements simple linked-list based allocation:

<ol>
<li>The size of the block we are looking for is the size that the user is requesting. (Note: if this size in bytes is over SBRK SIZE – TOTAL METADATA SIZE, set my malloc errno to the error SINGLE REQUEST TOO LARGE and return NULL</li>
<li>If the request size is 0, we do not have to allocate anything; mark NO ERROR and return NULL).</li>
<li>Now that we have the size we care about, we need to iterate through our freelist to find a block that best fits. Best fit is defined as the first block that has the same user data size as the requested amount of bytes, or the smallest block that has more than enough space for the requested data.
<ol>
<li>(a) &nbsp;If the best fit block is exactly the same size, you can simply remove it from the addr list and return a pointer to the body of the block to the user.</li>
<li>(b) &nbsp;If the best fit block is larger than the requested size, but is not big enough to split, then simply remove and return the block, as if it were a perfect fit. To tell if a block is too small to split, take the user data size of the original block and subtract the number of requested bytes. If the remaining number of bytes is not enough to contain a valid block of metadata size + 1 user byte (defined as MIN_BLOCK_SIZE), then it is too small to split.</li>
<li>(c) &nbsp;If the block is big enough to house a new block, we need to split off the portion we will use from the right side of the block, keeping the remaining left side in the freelist. Remember: pointer arithmetic can be tricky, so make sure you are casting to a uint8 t * before adding the total size (measured in bytes) to find the split pointer! Otherwise, your calculations might get implicitly multiplied by sizeof(metadata_t).</li>
</ol>
If no suitable blocks are found at all (i.e., all blocks have a user data size smaller than the requested size), then call my sbrk() with the size SBRK SIZE to get more memory. Our autograder expects exactly this amount of size to be requested, so please make sure to use the macro.

The chunk of memory returned by my sbrk() should be treated as a new block, so you will need to write a metadata t to the start of the block. This means that the block’s available user size is actually SBRK_SIZE – TMS.

Additionally, you must merge this new block with any free blocks that are directly next to the new block in the freelist. Since the freelist is sorted by address, there is only one block you need to check: the last block in the freelist. However, you may find it easier to repurpose some of your code from my_free(); you can even call my_free() on the newly sbrk’d block in order to put it back, but you will need a working implementation of my_free() first.
</li>
</ol>
</div>
</div>
<div class="layoutArea">
<div class="column">
9

</div>
</div>
</div>
<div class="page" title="Page 10">
<div class="layoutArea">
<div class="column">
4.

2.7

</div>
<div class="column">
After setting up the block’s metadata and merging it if possible, restart the search for a best-fit block. In the event that my sbrk() returns failure (by returning NULL), you should set the error code OUT OF MEMORY and return NULL.

Remember that you want the address you return to be at the start of the block body, not the metadata. This is sizeof (metadata t) bytes away from the very front of the block. Since pointer arithmetic is in multiples of the sizeof the data type, you can just add 1 to a pointer of type metadata t* pointing to the front of the metadata to get a pointer to the body. If you have not specifically set the error code during this operation, set the error code to NO ERROR before returning.

The first call to my malloc() should call my sbrk(). Note that malloc should call my sbrk() when it doesn’t have a block to satisfy the user’s request anyway, so this isn’t a special case.

my free()

</div>
</div>
<div class="layoutArea">
<div class="column">
You are also to write your own version of free that implements deallocation. This means:

<ol>
<li>Calculate the proper address of the block to be freed, keeping in mind that the pointer passed to any
call of my free() is a pointer to the block’s user data section and not to the block’s metadata.
</li>
<li>Attempt to merge the block with blocks that are next to it if those blocks are free. See the previous
subsection on deallocating for more information on how to do this.
</li>
<li>Finally, place the resulting block in the addr list by setting the respective next pointer in each node
for the addr list. Do not forget to keep the list sorted by address.
</li>
</ol>
Just like the free() in the C standard library, if the pointer is NULL, no operation should be performed.

2.8 my realloc()

You are to write your own version of realloc that will use your my malloc() and my free() functions. my realloc() should accept two parameters from the user, void *ptr and size t size. It will attempt to effectively change the size of the memory block pointed to by ptr to size bytes, and return a pointer to the beginning of the new memory block.

Do not directly change the freelist or blocks in my realloc() — leave that to my malloc() and my free(). This means you don’t need to worry about shrinking or extending blocks in place1; if size is nonzero, just call my malloc() to attempt to allocate a new block of the new size. Make sure to copy as much data as will fit in the new block from the old block to the new block (don’t forget to eventually free the old pointer). The rest of the data in the new block (if any) should be uninitialized.

Your my realloc() implementation must have the same features as the realloc() function in the standard library. Specifically:

<ol>
<li>If the pointer is null, call my malloc using the size argument (i.e. my malloc(size))</li>
<li>If the size is equal to zero, and pointer is non-null, call my freefree using the ptr argument and return
null (i.e. my free(ptr))
</li>
<li>Else, create a new block via my malloc and and copy the old block’s data to the new block up to
min(new block data size, old block data size)
</li>
<li>If the requested size is nonzero and my malloc fails, then do not free the old pointer.</li>
</ol>
Hint: Look at the man page for the C function memcpy

1Even though we don’t extend or shrink blocks in place in this homework, keep in mind that real-world implementations (which are not written in a panic right before finals) very well could.

</div>
</div>
<div class="layoutArea">
<div class="column">
10

</div>
</div>
</div>
<div class="page" title="Page 11">
<div class="layoutArea">
<div class="column">
2.9 my calloc()

You are to write your own version of calloc that will use your my malloc() function. my calloc() should accept two parameters, size t nmemb and size t size. It will allocate a region of memory for nmemb number of elements, each of size size, zero out the entire block, and return a pointer to that block.

If my malloc() returns NULL, do not set any error codes (as my malloc() will have taken care of that) and just return NULL directly.

Hint: Look at the man page for the C function memset

2.10 Error Codes

For this assignment, you will also need to handle cases where users of your malloc do improper things with their code. For instance, if a user asks for 12 gigabytes of memory, this will clearly be too much for your 8 kilobyte heap. It is important to let the user know what they are doing wrong. This is where the enum in the my malloc.h comes into play. You will see the four types of error codes for this assignment listed inside

</div>
</div>
<div class="layoutArea">
<div class="column">
of it.

• • •

</div>
<div class="column">
They are as follows:

NO ERROR: set whenever my calloc(), my malloc(), my realloc(), and my free() complete suc- cessfully.

OUT OF MEMORY: set whenever the user’s request cannot be met because there’s not enough heap space.

SINGLE REQUEST TOO LARGE: set whenever the user’s requested size plus the total metadata size is beyond SBRK SIZE.

</div>
</div>
<div class="layoutArea">
<div class="column">
Inside the .h file, you will see a variable of type enum my malloc err called my malloc errno. Whenever any of the cases above occur, you are to set this variable to the appropriate type of error. You may be wondering what happens if a single request is too large AND it causes malloc to run out of memory. In this case, we will let the SINGLE REQUEST TOO LARGE take precedence over OUT OF MEMORY. So in the case of a request of 9kb, which is clearly beyond our biggest block and total heap size, we set ERRNO to SINGLE REQUEST TOO LARGE.

2.11 Suggested Helper Methods

Coding malloc can seem like quite a daunting challenge, but your debugging process can be helped along tremendously if you do not write all of malloc in one method and instead split it up into helper methods! Helper methods are incredibly useful for understanding what is going on and also results in cleaner code, so it’s a win-win strategy. Below are some TA recommended helper methods to implement, and while they are not required and will not be tested with the autograder, we advise that you use them.

All helper methods must be declared static:

• static metadata_t* find_right(metadata_t*)

• static metadata_t* find_left(metadata_t*)

• static void merge(metadata_t* left, metadata_t* right)

• static metadata_t* split_block(metadata_t* block, size_t size) • static void add_to_addr_list(metadata_t* add_block)

• static void remove_from_addr_list(metadata_t* remove_block)

• static metadata_t* find_best_fit(size_t size);

</div>
</div>
<div class="layoutArea">
<div class="column">
11

</div>
</div>
</div>
<div class="page" title="Page 12">
<div class="layoutArea">
<div class="column">
Remember, this is not an exhaustive list of operations that can performed with helper methods. Feel free to implement helper methods for any aspect of malloc that works for you.

Note: We are declaring these functions to be static because we want them to be private to my malloc.c. DO NOT put any function prototypes in my malloc.h

2.12 Running the Autograder and Debugging

If you are not on Docker, before running the Makefile, you need to install Check, a C unit testing library used by the autograder.

To run the autograder’s test suite, run:

<pre>    # Run all test cases
    $ make run-tests
</pre>
<pre>    # Run a specific test case
    $ make run-tests TEST=Malloc_Perf_Block1
</pre>
When you run the tests, you will see a pretty hefty output in your terminal. Each line of the output provides critical information depicting which tests you are failing/passing. The general format of:

suite filename.c:420:Fun Test Case:test description

states a test named test description is failing/passing in an individual test case named Fun Test Case, located in that specific test suite suite filename.c at line 420. That is, test suites contain test cases which contain tests. For example,

malloc suite.c:37:Malloc Perf Block1:test malloc perf block1 lists

tells us whether the address list and size list is correct when we malloc for a perfectly sized block. More information about the test is written in malloc suite.c, and the assertion that failed is on line 37.

To run an individual test case, run

<pre>    $ make run-tests TEST=Malloc_Init
</pre>
To debug an individual test case with gdb, run

<pre>    $ make run-gdb TEST=Malloc_Split_Block_SBRKmerge
</pre>
2.13 Deliverables

Submit the following files to the “Homework 10: Malloc Implementation” assignment on Gradescope:

• my malloc.c

Do NOT modify or submit the header file, my malloc.h. We will grade with the original copy. Any functions

or variables you add should be marked static so they do not conflict with the grader.

Note that we reserve the right to change test case weighting or add additional test cases to the autograder after the assignment is due.

</div>
</div>
<div class="layoutArea">
<div class="column">
12

</div>
</div>
</div>
<div class="page" title="Page 13">
<div class="layoutArea">
<div class="column">
3

1.

</div>
<div class="column">
Frequently Asked Questions

I have a segfault, what do I do?

The quickest way is to debug it yourself with gdb. Here is the link to our supplemental gdb video:

• https://www.youtube.com/watch?v=GMF2tpXVKqQ Here are some other gdb tutorials:

<ul>
<li>https://www.youtube.com/playlist?list=PLsK1fComPkFiYc4oX8Ef9QUyiWVM5BaKe(playlistcre- ated by a previous TA)</li>
<li>https://www.cs.cmu.edu/~gilpin/tutorial/</li>
<li>http://www.cs.yale.edu/homes/aspnes/pinewiki/C%282f%29Debugging.html</li>
<li>http://heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Debug.html</li>
<li>http://heather.cs.ucdavis.edu/~matloff/debug.html</li>
<li>http://www.delorie.com/gnu/docs/gdb/gdb_toc.html
Can we build our freelists with list heads/dummy nodes?

No; the autograder checks the state of the freelist and will fail if you have dummy nodes.

Should we first initialize the freelist to NULL?

No, it is static and is therefore already initialized to NULL by the compiler.

Are the provided tests comprehensive?

Yes. We reserve the right to change our mind on this, but if you get a 100 on Gradescope, you should expect 100 on the homework. Just keep in mind that the tests may be weighted differently when grading than in the provided student autograder.

Rules and Regulations General Rules

Although you may ask TAs for clarification, you are ultimately responsible for what you submit. As such, please start assignments early, and ask for help early. This means that (in the case of demos) you should come prepared to explain to the TA how any piece of code you submitted works, even if you copied it from the book or read about it on the internet.

If you find any problems with the assignment it would be greatly appreciated if you reported them to the TAs. Announcements will be posted if the assignment changes.
</li>
</ul>
</div>
</div>
</div>
<div class="page" title="Page 14">
<div class="layoutArea">
<div class="column">
&nbsp;

</div>
</div>
</div>
