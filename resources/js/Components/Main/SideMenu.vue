<script setup>
import { Link } from '@inertiajs/vue3';
import { Badge } from '@/Components/ui/badge'
import { Button } from '@/Components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/Components/ui/card'
import { Bell, Home, LineChart, Package, PlaneTakeoff, ShoppingCart, Users } from 'lucide-vue-next'

</script>
<template>
    <nav class="hidden border-r bg-muted/40 md:block">
        <div class="flex h-full max-h-screen flex-col gap-2">
            <div class="flex h-14 items-center border-b px-4 lg:h-[60px] lg:px-6">
                <Link to="/dashboard" class="flex items-center gap-2 font-semibold">
                <PlaneTakeoff class="h-6 w-6" />
                <span class="">Larajet</span>
                </Link>
                <Button variant="outline" size="icon" class="ml-auto h-8 w-8">
                    <Bell class="h-4 w-4" />
                    <span class="sr-only">Toggle notifications</span>
                </Button>
            </div>
            <div class="flex-1">
                <nav class="grid items-start px-2 text-sm font-medium lg:px-4">
                    <Link to="/dashboard"
                        class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all hover:text-primary"
                        :class="route().current('dashboard') ? 'bg-muted text-primary' : 'text-muted-foreground'">
                    <Home class="h-4 w-4" />
                    Dashboard
                    </Link>
                    <a href="#"
                        class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all hover:text-primary">
                        <ShoppingCart class="h-4 w-4" />
                        Orders
                        <Badge class="ml-auto flex h-6 w-6 shrink-0 items-center justify-center rounded-full">
                            6
                        </Badge>
                    </a>
                    <a href="#"
                        class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all hover:text-primary">
                        <Package class="h-4 w-4" />
                        Products
                    </a>
                    <a href="#"
                        class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all hover:text-primary">
                        <Users class="h-4 w-4" />
                        Customers
                    </a>
                    <a href="#"
                        class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all hover:text-primary">
                        <LineChart class="h-4 w-4" />
                        Analytics
                    </a>
                </nav>
            </div>
            <div class="mt-auto p-4">
                <Card>
                    <CardHeader class="p-2 pt-0 md:p-4">
                        <CardTitle>Upgrade to Pro</CardTitle>
                        <CardDescription>
                            Unlock all features and get unlimited access to our support
                            team.
                        </CardDescription>
                    </CardHeader>
                    <CardContent class="p-2 pt-0 md:p-4 md:pt-0">
                        <Button size="sm" class="w-full">
                            Upgrade
                        </Button>
                    </CardContent>
                </Card>
            </div>
        </div>
    </nav>
</template>