<div>
        <p>The following errors haven't yet been fixed in any printing.</p>
	<ol>
	<li>The bibliography is missing an entry for Bovet &amp; Cesati [2006], which is mentioned on page 74.  The reference should be:<br>
Bovet, D. P. and Cesati, M. <em>Understanding the Linux Kernel, Third Edition</em>.  O'Reilly Media, Sebastopol, CA.</li>
	<li>On page 929 (Appendix C), Exercise 13.3 should be labeled 13.4.</li>
	<li>Pages 307 and 309 refer to Figure 9.13.  It should be 9.12.</li>
	<li>On page 842, the <span class="style1">printer_status</span> function has a bug that will potentially affect RISC-based platforms when the IPP header isn't aligned properly.  Instead of
<pre>    struct ipp_hdr *hp;
    hp = (struct ipp_hdr *)cp;
    i = ntohs(hp-&gt;status);
    jobid = ntohl(hp-&gt;request_id);
</pre>
the code should be
<pre>    struct ipp_hdr h;
    memcpy(&amp;h, cp, sizeof(struct ipp_hdr));
    i = ntohs(h.status);
    jobid = ntohl(h.request_id);
</pre></li>
        <li>Figure 17.14 exposes a bug in most 64-bit versions of Linux that results in <span class="style1">msg_controllen</span> being updated improperly.  To work around the problem, change
<pre>        if (msg.msg_controllen != CONTROLLEN)
</pre>
to
<pre>	if (msg.msg_controllen &lt; CONTROLLEN)
</pre>
        The same problem affects <span class="style1">lib/recvfd.c</span> in the source code for the APUE library.
        </li>
	<li>The <span class="style1">add_worker</span> function on page 828 doesn't set up the linked list properly.  The problem only shows up when there is more than one request being processed at the same time.  Instead of
<pre>    if (workers == NULL)
        workers = wtp;
    else
        workers-&gt;prev = wtp;
</pre>
the code should be
<pre>    if (workers != NULL)
        workers-&gt;prev = wtp;
    workers = wtp;
</pre></li>
	<li>Figure 16.4 on page 592 lists section 3.3 as the reference for <span class="style1">close</span>.  It should be section 3.5.</li>
	<li>On page 305, the second line from the top contains the phrase "encrypted correctly;" it should be "decrypted correctly" (the cited example is using the <span class="style1">crypt</span> command to decrypt the file for printing).</li>
	<li>On pages 127 and 910, references to the <span class="style1">utime</span> function should instead refer to the <span class="style1">utimes</span> function.</li>
	<li>On page 148, the last paragraph refers to Figure 5.3.  It should be Figure 5.2.</li>
	<li>On page 331, the last sentence before the example refers to <span class="style1">sigsetjmp</span>.  It should be <span class="style1">siglongjmp</span>.</li>
	<li>On page 416, the reference to <span class="style1">cond_signal</span> should instead be <span class="style1">pthread_cond_signal</span>.</li>
	<li>On page 493, the locks are linked from the v-node structure, not the i-node structure.</li>
	<li>On page 632, the last sentence begins with "Well," but it should be "We'll."</li>
	<li>On page 834, "Universal Resource Identifier" should be "Uniform Resource Identifier."</li>
	<li>On page 957, "<span class="style1">cat</span> constant" should be removed.</li>
	<li>On page 982, "<span class="style1">_SC_NZERO</span> function" should be "<span class="style1">_SC_NZERO</span> constant."</li>
	<li>On page 321, in the description for <span class="style1">SIGTTOU</span>, <span class="style1">write</span> will fail as described only in case (b).</li>
	<li>On page 378, the <span class="style1">sig_tstp</span> signal handler has a race.  It shouldn't unblock <span class="style1">SIGTSTP</span> until after the call to <span class="style1">kill</span>.</li>
	<li>On page 950, <em>The Linux Programming Interface</em> is published by No Starch Press (not "No Startch Press").</li>
	<li>On the first line on page 639, the argument to <span class="style1">malloc</span> is <span class="style1">sizeof(un.sun_path + 1)</span>, but it should be <span class="style1">sizeof(un.sun_path) + 1</span>.</li>
	<li>On page 250, the third full paragraph from the bottom of the page ends with "three functions."  It should be "four functions."</li>
	<li>On page 252, the discussion of the <span class="style1">type -f</span> option for the <span class="style1">find</span> command should be the <span class="style1">-type f</span> option.</li>
	<li>On page 111, the description of the <span class="style1">du</span> command's behavior is reversed.  When the <span class="style1">POSIXLY_CORRECT</span> environment variable is set, <span class="style1">du</span> reports 512-byte block units.  Otherwise, it defaults to 1,024-byte units.</li>
	</ol>
      </div>
